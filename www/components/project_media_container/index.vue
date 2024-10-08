<template>
    <div> 
        <div v-if="props.project.mediaType == 'image'">
            <img :src="props.project.media" alt="project media" />
        </div>
        <div v-else-if="props.project.mediaType == 'video'">
            <iframe :src="props.project.media" frameborder="0" allowfullscreen
                />
        </div>
     </div>
</template>

<script setup lang="ts">

import { defineProps } from "vue";

const props = defineProps<{
  project: {
    name: string;
    media: string;
    mediaType: string;
  };
}>();


</script>

<style></style>