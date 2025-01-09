<script setup lang="ts">
import { ref, onMounted } from 'vue'
const props = defineProps<{ countryCode: string }>()
const cityInfo = ref<City[]>([])
onMounted(async () => {
  const res = await fetch('/api/country/' + props.countryCode)
  if (res.ok) {
    cityInfo.value = await res.json()
  }
})

interface ValidString {
    String: string
    Valid: boolean
}

interface ValidNumber {
    Int64: number
    Valid: boolean
}

interface City {
    id: number
    name: ValidString
    countryCode: ValidString
    district: ValidString
    population: ValidNumber
}
</script>

<template>
  <div>
    <h1>
      {{ countryCode }}
    </h1>
    <div>
        <ul>
            <li v-for="city in cityInfo" :key="city.id">
                <router-link :to="{path: `../city/${city.name.String}`}">{{ city.name.String }}</router-link>
            </li>
        </ul>
    </div>
    <div v-if="cityInfo">{{ cityInfo }}</div>
    <div v-else>国が見つかりませんでした</div>
  </div>
</template>