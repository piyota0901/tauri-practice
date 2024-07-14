<script setup lang="ts">
import { reactive, ref, onMounted } from 'vue';
import Profile from './Profile.vue';
import Search from './Search.vue';
import type { VueElement } from 'vue';
import type { MenuItemType } from 'ant-design-vue/es/menu/src/hooks/useItems';

function getItem(
  label: VueElement | string,
  key: string,
  icon?: any,
  children?: MenuItemType[],
  type?: 'group',
): MenuItemType {
  return {
    key,
    icon,
    children,
    label,
    type,
  } as MenuItemType;
}

const menuItems = reactive<MenuItemType[]>([
  getItem('Todo', 'grp', null, [getItem('Project A', '1', ), getItem('Project B', '2')], 'group')
]);

const selectedKeys = ref<string[]>(['1']);

// --------------------------------------------
// サイドバーの幅のリサイズ処理
// --------------------------------------------
const sidebarWidth = ref(250);
const isDragging = ref(false);

const stopDrag = () => {
  console.log('stopDrag');
  isDragging.value = false;
  document.body.style.userSelect = '';
}

const startResize = (event: MouseEvent) => {
  if (isDragging.value) {
    let width = event.clientX;
    const cursor_speed = 1.08;
    if (width < 250) {
      width = 250;
    } else if (width > 400) {
      width = 400;
    } else {
      width = width * cursor_speed;
    }
    sidebarWidth.value = width;
  }
}

onMounted(() => {
  const resizer = document.querySelector('.resizer');
  resizer!.addEventListener('mousedown', () => {
    console.log('startDrag');
    document.body.style.userSelect = 'none';
    isDragging.value = true;
    
    document.addEventListener('mousemove', startResize); // document全体とすることで、resizerの外側でもドラッグできるようにする
    document.addEventListener('mouseup', stopDrag); // ドラッグ終了時の処理
  });
});

</script>
<template>
<a-layout-sider
  theme="light"
  width="360"
>
  <!-- Profile -->
  <Profile 
    username="John Doe" 
    email="john.d@example.com"
  />
  <Search />
  <a-divider style="margin: 0 0;"/>
  <a-menu 
    v-model:selectedKeys="selectedKeys" 
    :items="menuItems"
  ></a-menu>
</a-layout-sider>
<div class="resizer">
</div>
</template>
<style scoped>
.resizer {
  width: 4px;
  background: rgb(14, 214, 131);
  cursor: col-resize;
}
</style>