<template>
  <div>
    <label for="primary-color">Select Primary Color:</label>
    <select id="primary-color" v-model="selectedPrimary" @change="updateColors">
      <option value="lime">Lime</option>
      <option value="blue">Blue</option>
      <option value="red">Red</option>
      <option value="green">Green</option>
      <option value="purple">Purple</option>
      <option value="orange">Orange</option>
    </select>

    <label for="gray-color">Select Gray Color:</label>
    <select id="gray-color" v-model="selectedGray" @change="updateColors">
      <option value="neutral">Neutral</option>
      <option value="gray-500">Gray 500</option>
      <option value="gray-700">Gray 700</option>
      <option value="gray-300">Gray 300</option>
      <option value="gray-900">Gray 900</option>
    </select>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const appConfig = useAppConfig();
const selectedPrimary = ref('lime')
const selectedGray = ref('neutral')

const updateColors = () => {
  appConfig.ui.primary = selectedPrimary.value
  appConfig.ui.gray = selectedGray.value
}
</script>

<style scoped>
/* Add any additional styles here */
</style>
