<script setup lang="ts">
import HelloWorld from '../components/HelloWorld.vue'
import { ref } from 'vue'

const city = ref<string>('')
</script>

<template>
  <div>
    <div>
      <input type="text" v-model="city" placeholder="City Name" />
      <button @click="() => $router.push('/city/' + city)">Search</button>
    </div>
    <hello-world msg="Hello Vue 3 + Vite" />
  </div>
</template>