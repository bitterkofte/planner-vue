//TEMPLATE
<template>
  <div class="project">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons">edit </span>
        <span @click="deleteHandler" class="material-icons"> delete_forever </span>
        <span class="material-icons"> done </span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

//SCRIPT
<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import { defineEmits } from 'vue'

const emit = defineEmits(["delete"]);
const props = defineProps(["project"]);

let showDetails = ref(false);
const uri = `http://localhost:3000/projects/${props.project.id}`

const deleteHandler = () => {
  fetch(uri, { method: 'DELETE' })
  .then(() => emit('delete', props.project.id))
  .catch(err => console.error(err.message))
}

// onMounted(() => console.log('ONMOUNTED!!!'))
// onUnmounted(() => console.log("unmounted"))
</script>

//STYLE
<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
  user-select: none;
  transition: all 400ms;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.icons>* {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
  transition: all 200ms;
}
.material-icons:nth-child(1):hover {
  transform: scale(1.07);
  color: #ded421;
  text-shadow: 
    0 0 7px #fffb89,
    0 0 10px #fffc9e,
    0 0 15px #fffeb4,
    0 0 23px #feffb6;
}
.material-icons:nth-child(2):hover {
  transform: scale(1.07);
  color: #c21b1b;
  text-shadow: 
    0 0 7px #ff8989,
    0 0 10px #ff9e9e,
    0 0 15px #ffb4b4,
    0 0 23px #ffb6b6;
}
.material-icons:nth-child(3):hover {
  transform: scale(1.07);
  color: #1cbb31;
  text-shadow: 
    0 0 7px #89ff8f,
    0 0 10px #9effa0,
    0 0 15px #b4ffb9,
    0 0 23px #b6ffb9;
}
</style>
