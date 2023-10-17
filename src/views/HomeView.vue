<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <ProjectCard :project="project" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import ProjectCard from '@/components/ProjectCard.vue'
let projects = ref([]);

onMounted(() => {
  fetch('http://localhost:3000/projects')
  .then(res => res.json())
  .then(data => projects.value = data)
  .catch(err => console.error(err.message))
})
</script>
