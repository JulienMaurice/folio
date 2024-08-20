<template>
  <div class="flex items-center">
    <UBadge :color="getColor" class="text-xs" v-bind="$attrs">
      <UIcon :name="getIcon" class="mr-1" />
      {{ label }}
    </UBadge>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  status: 'beta' | 'paused' | 'solo'
}>()

const label = computed(() => {
  switch (props.status) {
    case 'beta':
      return 'Beta'
    case 'paused':
      return 'Paused'
    case 'solo':
      return 'Solo Dev'
    default:
      return ''
  }
})

const getColor = computed(() => {
  switch (props.status) {
    case 'beta':
      return 'yellow'
    case 'paused':
      return 'gray'
    case 'solo':
      return 'green'
    default:
      return 'gray'
  }
})

const getIcon = computed(() => {
  switch (props.status) {
    case 'beta':
      return 'i-heroicons-code-bracket'; 
    case 'paused':
      return 'i-heroicons-pause'; 
    case 'solo':
      return 'i-heroicons-computer-desktop'; 
    default:
      return '';
  }
})
</script>
