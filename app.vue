<template>
  <div>
    <UContainer>
      <UCard class="mt-10">
        <template #header>
          <div class="flex justify-between items-center">
            <h1 class="text-2xl font-thin">Dev.</h1>
            <DarkModeToggle />
          </div>
        </template>
      </UCard>
    </UContainer>

    <UContainer class="py-10">
      <div class="flex flex-col md:flex-row gap-10">
        <!-- Left side: Profile -->
        <div class="w-full md:w-1/3">
          <ProfileCard
            :github-profile-image="githubProfileImage"
            :name="name"
            :location="location"
            :technologies="technologies"
            :social-links="socialLinks"
          />
        </div>

        <!-- Right side: Projects -->
        <div class="w-full md:w-2/3">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <ProjectCard
              v-for="project in projects" :key="project.name"
              :project="project"
              />
          </div>
        </div>
      </div>
    </UContainer>
  </div>
</template>

<script setup>
import projects from '~/static/projects.json'

const name = 'Julien Maurice Veltre'
const location = 'France'
const githubProfileImage = 'https://avatars.githubusercontent.com/u/68739585?v=4'

const technologies = [
  'https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vue.js&logoColor=4FC08D',
  'https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white',
  'https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white',
  'https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black',
  'https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white',
]

const socialLinks = [
  { name: 'GitHub', icon: 'i-simple-icons-github', url: 'https://github.com/JulienMaurice' },
  { name: 'GitLab', icon: 'i-simple-icons-gitlab', url: 'https://gitlab.com/julien.maurice' },
  { name: 'LinkedIn', icon: 'i-simple-icons-linkedin', url: 'https://www.linkedin.com/in/julien-maurice/' },
  { name: 'Email', icon: 'i-heroicons-envelope', url: 'mailto:ju.maurice95@gmail.com' },
]

</script>
