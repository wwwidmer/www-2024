<template>
  <header class="header">
    <nav>
      <ul>
        <li><a href="/about">About</a></li>
        <li><a href="/projects">Projects</a></li>
        <li><a :href="resumeLink" target="_blank">Resume</a></li>
      </ul>
    </nav>
  </header>
</template>

<script setup lang="ts">
const content = await queryContent("/data").findOne();

const resumeLink = content.resumeLink;
</script>
