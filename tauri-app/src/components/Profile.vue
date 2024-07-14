<script setup lang="ts">
import { UserOutlined } from '@ant-design/icons-vue';

interface Props {
  username: string;
  email: string;
  avatarColor?: string;
}

withDefaults(defineProps<Props>(), {
  avatarColor: '#f56a00'
});

</script>
<template>
  <a-card 
    :bodyStyle="{ padding: '12px' }"
    :bordered="false"
    style="
      box-shadow: none; 
      border-radius: 0;
      background-color: var(--avatar-bg-color);
    "
  >
    <a-space style="align-items: center; ">
      <a-avatar 
        :style="{verticalAlign: 'middle', backgroundColor: avatarColor}" 
        size="large"
      >
        <template #icon>
          <UserOutlined />
        </template>
      </a-avatar>
      <div>
        <div class="name">{{ username }}</div>
        <div class="email">{{ email }}</div>
      </div>
    </a-space>
  </a-card>
</template>
<style scoped>
</style>