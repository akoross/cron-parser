<script setup lang="ts">
import {onMounted, ref, watch} from 'vue'
import cronstrue from 'cronstrue'

const inputCron = ref('5 * * * *')
const cronText = ref()

onMounted(() => {
  printCron()
})

watch(inputCron, () => {printCron()})

function printCron() {
  try {
    cronText.value = cronstrue.toString(inputCron.value)
  } catch (error: unknown) {
    cronText.value = error
  }
}

function auitCron() {
  const audit= inputCron.value.split(' ')
  if (audit.length > 5) {
    throw new Error('not use second')
  }
}
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
