<template>
  <UCard>
    <div class="text-left">
      <img :src="githubProfileImage" alt="GitHub Profile" class="w-72 h-72 rounded-full mx-auto mb-4">
      <h2 class="text-2xl font-bold mb-2">{{ name }}</h2>
      <div class="flex items-center mb-2">
        <UIcon name="i-heroicons-map-pin" class="mr-2" />
        <span>{{ location }}</span>
      </div>
      <div class="text-sm italic mb-4 flex items-center">
        <UIcon name="i-heroicons-academic-cap" class="mr-2" />
        <span>Ex military came to tech</span>
      </div>
      <div class="flex flex-wrap gap-2 mb-4">
        <img v-for="tech in technologies" :key="tech" :src="tech" :alt="tech" class="h-6">
      </div>
    
      <!-- Social Links -->
      <div class="flex flex-wrap justify-center gap-4 mt-4">
        <UButton
          v-for="link in socialLinks" :key="link.name" :icon="link.icon" :to="link.url" target="_blank"
          color="gray" variant="ghost" class="text-3xl p-3" />
      </div>
    </div>
  </UCard>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  githubProfileImage: {
    type: String,
    default: 'https://avatars.githubusercontent.com/u/68739585?v=4'
  },
  name: {
    type: String,
    default: 'Julien Maurice'
  },
  location: {
    type: String,
    default: 'France'
  },
  technologies: {
    type: Array,
    default: () => [
    ]
  },
  socialLinks: {
    type: Array,
    default: () => [
    ]
  }
})
</script>
