<template>
  <div class="home">
    <FilterNavbar :current="current" @filterChange="current = $event"/>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <ProjectCard :project="project" @delete="deleteHandler" @complete="toggleComplete" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import ProjectCard from '@/components/ProjectCard.vue'
import FilterNavbar from '@/components/FilterNavbar.vue'
let projects = ref([]);
let current = ref('all');

onMounted(() => {
  fetch('http://localhost:3000/projects')
  .then(res => res.json())
  .then(data => projects.value = data)
  .catch(err => console.error(err.message))
})

const deleteHandler = (id) => {
  projects.value = projects.value.filter(p => p.id !== id)
}
const toggleComplete = (id) => {
  let p = projects.value.find(pro => pro.id === id)
  p.complete = !p.complete
  // projects.value = projects.value.map(p => p.id === id ? p.complete = !p.complete : "")
}
</script>
