<template>
  <div v-if="project" class="page-container">
    <h1>{{ project.name }}</h1>
    <div class="project-container">
      <div class="description">{{ project.longDescription }}</div>

      <div class="tags">
        <ProjectMediaContainer :project="project" />
        <ul>
          <li v-for="tag in project.tags" :key="tag">
            {{ tag }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const content = await queryContent("/projects").findOne();
const projects = content.data;
const route = useRoute();
const project = projects[route.params.slug as string];

if (!project && import.meta.server) {
  const event = useRequestEvent();
  if (!event) {
    throw new Error("No request event found");
  }
  setResponseStatus(event, 404);
  setResponseStatus(event, 404, "Page Not Found");
}
</script>

<style>
.page-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.project-container {
  display: flex;
  flex-direction: row;
  align-items: center;

  .description {
    max-width: 33vw;
  }

  .tags {
    > ul {
      list-style: none;
      display: flex;

      > li {
        text-transform: capitalize;
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 0.5rem;
        margin-right: 0.5rem;
      }
    }
  }
}
</style>
