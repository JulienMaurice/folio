<template>
  <UCard class="cursor-pointer flex flex-col h-full transition-transform hover:scale-105"        @click="openModal"
  >
    <template #header>
      <div class="relative overflow-hidden h-48">
        <NuxtImg :src="project.image" :alt="project.name" class="w-full h-full object-cover transform scale-110" />
        <div class="absolute inset-0 bg-black opacity-0 dark:opacity-30 transition-opacity" />
      </div>
    </template>
    <div class="flex flex-col px-2 h-full">
      <div class="flex mb-2 flex-col sm:flex-row sm:justify-between sm:items-center">
        <div class="flex items-center mb-2 sm:mb-0">
          <UIcon :name="project.icon" class="mr-2 text-xl sm:text-2xl" />
          <h3 class="text-base font-semibold">{{ project.name }}</h3>
        </div>

        <div class="flex flex-wrap gap-1 ml-3 justify-end">
          <ProjectStatusTag 
            v-for="status in project.statuses" 
            :key="status" 
            :status="status"
          />
        </div>
      </div>

      <div class="min-h-20">

        <p class="text-sm mb-2" :title="project.quickDescription">{{ project.quickDescription }}</p>
      </div>

      <a s:href="project.link" target="_blank" rel="noopener noreferrer">
          <img :src="project.linkImage" :alt="project.name" class="h-7">
      </a>
    </div>
  </UCard>

  <ProjectModal v-model="modal" :project="project" />
</template>

<script setup>
defineProps({
  project: {
    type: Object,
    required: true
  }
})

const modal = ref(false);
const openModal = () => {
  modal.value = true
}
</script>
