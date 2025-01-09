<script setup lang="ts">
import { ref, onMounted } from 'vue'

const countries = ref<Country[]>([])
onMounted(async () => {
  const res = await fetch('/api/world')
  if (res.ok) {
    countries.value = await res.json()
  }
})

interface Country {
  code: string
  name: string
}

</script>

<template>
  <div>
    <h1>
      World
    </h1>
    <div v-if="countries">
      <ul>
        <li v-for="country in countries" :key="country.code">
          <router-link :to="{path: `country/${country.code}`}">{{ country.name }}</router-link>
        </li>
      </ul>
    </div>
    <div v-else>ワールドが見つかりませんでした</div>
  </div>
</template>