<template>
  <UModal v-model="isOpen">
    <UCard
>
      <template #header>
        <div class="flex justify-between items-center">
          <div class="flex items-center">
            <UIcon :name="project.icon" class="mr-2 text-2xl" />
            <h3 class="text-xl font-semibold mr-2">{{ project.name }}</h3>
          </div>

          <div class="flex">
            <div class="flex space-x-1 mr-1">
              <ProjectStatusTag v-for="status in project.statuses" :key="status" variant="soft" :status="status" />
            </div>
            <UButton icon="i-heroicons-x-mark" color="gray" variant="ghost" @click="close" />
          </div>
        </div>
      </template>
    

      <UCarousel
        v-slot="{ item }"
        :items="project.content"
        :ui="{
          item: 'basis-full'
        }"
        class="overflow-hidden w-full"
        arrows
        indicators
      >
        <div class="relative group aspect-video">
          <NuxtImg
            v-if="item.type === 'image'"
            :src="item.url"
            :alt="item.alt || ''"
            class="w-full h-full object-cover rounded-lg"
            loading="lazy"
          />
          <video 
            v-else-if="item.type === 'video'" 
            controls 
            class="w-full h-full object-cover rounded-lg" 
            draggable="false"
          >
            <source :src="item.url" type="video/mp4">
            Your browser does not support the video tag.
          </video>
          <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity bg-black bg-opacity-50 rounded-lg">
            <UButton
              v-if="item.type === 'image'"
              icon="i-heroicons-magnifying-glass-plus"
              color="white"
              variant="ghost"
              @click.stop="openFullImage(item)"
            />
          </div>
        </div>
      </UCarousel>

      <template #footer>
        <div class="flex mt-6">
          <!-- Project Description and Timeline -->
          <div class="flex-grow space-y-4 pr-6">
            <p class="font-extralight">{{ project.description || project.quickDescription }}</p>
            
            <div v-if="project.timeline">
              <h4 class="font-semibold mb-2 text-sm">Project Timeline:</h4>
              <ul class="space-y-2 text-xs">
                <li v-for="(item, index) in project.timeline" :key="index" class="flex items-start">
                  <div class="w-3 h-3 rounded-full bg-blue-500 mr-2 mt-0.5"/>
                  <div>
                    <span class="font-semibold">{{ item.date }}:</span>
                    <span> {{ item.event }}</span>
                    <p class="text-gray-600 mt-1">{{ item.description }}</p>
                  </div>
                </li>
              </ul>
            </div>

            <div v-if="project.presentation" class="pt-4">
              <UButton class="w-full flex justify-center items-center" color="primary" variant="outline" :to="project.presentation" target="_blank">View Presentation</UButton>
            </div>
          </div>
          
          <UDivider icon="i-heroicons-code-bracket" orientation="vertical"/>

          <!-- Technologies Used -->
          <div class="w-1/4 pl-6 flex items-center">
            <div class="flex flex-col space-y-4 items-center">
              <UTooltip v-for="tech in project.technologies" :key="tech.name" :text="tech.tooltip || tech.name">
                <UIcon :name="tech.icon" class="text-3xl" />
              </UTooltip>
            </div>
          </div>
        </div>
      </template>

      <!-- Full Image Modal -->
      <UModal v-model="isFullImageOpen" size="xl">
        <NuxtImg
          :src="fullImageSrc"
          :alt="fullImageAlt"
          class="max-w-full max-h-[90vh] object-contain"
          loading="lazy"
        />
      </UModal>
    </UCard>
  </UModal>
</template>

<script setup lang="ts">
const isFullImageOpen = ref(false)
const fullImageSrc = ref('')
const fullImageAlt = ref('')

function openFullImage(item: { url: string; alt?: string }) {
  fullImageSrc.value = item.url
  fullImageAlt.value = item.alt || ''
  isFullImageOpen.value = true
}

defineProps({
  project: {
    type: Object,
    required: true
  }
})

const isOpen = defineModel({default: false, type: Boolean})

const close = () => {
  isOpen.value = false
}
</script>
