<script setup lang="ts">
import {onMounted, ref, watch} from 'vue'
import cronstrue from 'cronstrue'

const inputCron = ref('* * * * * *')
const cronText = ref()

onMounted(() => {
  cronText.value = cronstrue.toString(inputCron.value)
})

const printCron = () => {
  try {
    cronText.value = cronstrue.toString(inputCron.value)
  } catch (error: unknown) {
    cronText.value = error
  }
}
watch(inputCron, async () => {
  try {
    cronText.value = cronstrue.toString(inputCron.value)
  } catch (error: unknown) {
    cronText.value = error
  }
})
</script>

<template>
    <input v-model="inputCron" @change="printCron" class="input" type="text">
    <p class="cron-info">{{ cronText }}</p>
</template>

<style lang="css" scoped>
.input {
  font-size: 1.5rem;
  text-align: center;
}
.cron-info {
  max-width: 320px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  font-size: 1.3rem;
  line-height: 1.7rem;
}
</style>
