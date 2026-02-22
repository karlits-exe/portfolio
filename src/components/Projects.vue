<script setup>
    import ProjectCard from './ProjectCard.vue';
    import projects from '../data/projects.json'

</script>

<template>
    <div id="projects" class="my-5">
      <div class="container">
        <div class="row g-3">
          <h1 class="text-center">My Projects</h1>
          <div class="col-12 col-md-6 col-lg-4 d-flex justify-content-center" v-for="project in projects" :key="project.id">
            <div v-if="project.isActive"> 
              <ProjectCard :project="project"/>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>