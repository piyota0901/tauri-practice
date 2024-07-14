<script setup lang="ts">
import { ref } from 'vue';
import { SearchOutlined } from '@ant-design/icons-vue';

const keyword = ref('');
</script>
<template>
<div style="display: flex; justify-content: center; margin-bottom: 10px;">
  <a-input
    v-model:value="keyword"
    placeholder="Search"
    style="width: 90%;"
  >
    <template #suffix>
      <search-outlined />
    </template>
  </a-input>
</div>
</template>