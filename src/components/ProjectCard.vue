<template>
  <div class="card">
    <img
      :src="project.image"
      class="card-img-top"
      alt="..."
    />
    <div class="card-body">
      <h5 class="card-title">{{ project.title }}</h5>
      <p class="card-text card-text-color">
        {{ project.description }}
      </p>
    </div>
    <div class="card-footer my-3" >
        <a :href="`#${project.link}`" class="rounded-3" id="project-link">View</a>

    </div>
  </div>
</template>

<script setup>
defineProps({
  project: Object,
});
</script>
