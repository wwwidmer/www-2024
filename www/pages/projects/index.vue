<template>
  <div class="about-container">
    <div> <p> Contained within are a subset of projects I have worked on at a variety of shops. Unfortunately much is proprietary so I can only give a high-level but I provide links when I can. Its impossible to share everything about every job I've worked in the last decade; This showcases my favorite projects with a slight recency bias.</p> </div>
    <div class="card-container">
      <div v-for="project in projects" :key="project.slug" class="card">
        <a :href="`/projects/${project.slug}`"> {{ project.name }}</a>
        <div>{{ project.shortDescription }}</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const content = await queryContent("/projects").findOne();
const projectsBySlug = content.data;

const projects = Object.keys(projectsBySlug).map((slug) => {
  return {
    slug,
    ...projectsBySlug[slug],
  };
});
</script>

<style>
.card-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  justify-content: center;
  align-items: center;
}

.card {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 1rem;
  margin-bottom: 1rem;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
