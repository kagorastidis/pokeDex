<!-- eslint-disable vue/multi-word-component-names -->

<script setup>
import { ref } from 'vue'

const props = defineProps(['pokemon'])

const backView = ref(false)

const toggleBackView = () => {
  backView.value = !backView.value
}
</script>

<template>
  <div class="pokemon" @click="toggleBackView">
    <div class="pokemon_front-view" v-if="!backView">
      <div class="pokemon__avatar">
        <img :src="props.pokemon.avatar" :alt="props.pokemon.name" />
      </div>
      <div class="pokemon__details">
        <div class="pokemon__id">#{{ props.pokemon.id }}</div>
        <div class="pokemon__name">
          {{ props.pokemon.name }}
        </div>
      </div>
    </div>
    <div class="pokemon__back-view" v-else>
      <div class="pokemon__details">
        <div class="pokemon__details-title">Stats:</div>
        <ul>
          <li v-for="(stat, index) in props.pokemon.stats" :key="index">
            {{ stat.stat.name }} : {{ stat.base_stat }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.pokemon {
  display: flex;
  flex-direction: column;
  background-color: rgb(216, 207, 207);
  box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.2);
  margin: 0 8px 32px 8px;
  padding: 24px 0;
  cursor: pointer;
  min-width: 250px;

  &__details {
    padding: 0 32px;

    &-title {
      font-size: 24px;
      font-weight: bolder;
      text-transform: capitalize;
    }

    ul {
      list-style-type: none;
      padding: 0;
    }
  }

  &__avatar {
    width: 200px;
    height: 200px;
    object-fit: cover;
    margin-bottom: 48px;

    img {
      border-radius: 50%;

      width: 100%;
      height: 100%;
    }
  }

  &__id {
    font-size: 18px;
    font-weight: bold;
  }

  &__name {
    font-size: 24px;
    font-weight: bolder;
    text-transform: capitalize;
  }
}
</style>
