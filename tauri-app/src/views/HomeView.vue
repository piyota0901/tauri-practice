<script setup lang="ts">
import Sidebar from '../components/Sidebar.vue';
import Header from '../components/Header.vue';
import Content from '../components/Content.vue';
</script>
<template>
<div class="container">
  <a-layout>
    <Sidebar />
    <a-layout>
      <Header />
      <Content />
    </a-layout>
  </a-layout>
</div>
</template>
<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>