<template>
  <div class="w-full h-full flex justify-center items-center">
    <div>
      <p>{{ joke.setup }}</p>
      <p v-show="!isDelivery"><button @click="isDelivery = true">Tell Me!</button></p>
      <div v-show="isDelivery">
        <p>{{ joke.delivery }}</p>
        <p><button @click="getJoke">Another</button></p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const joke = ref({})
const isDelivery = ref(false)


const getJoke = () => {
  fetch('https://v2.jokeapi.dev/joke/christmas')
    .then(res => res.json())
    .then(data => {
      joke.value = data
      isDelivery.value = false
    })
}
getJoke()
</script>

<style>
p {
  text-align: center;
}
</style>
