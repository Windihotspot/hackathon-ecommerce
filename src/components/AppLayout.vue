<template>
  <div class="min-h-screen h-full bg-gray-200 flex">
    <!-- Sidebar -->
    <Sidebar :class="{'-ml-[200px]': !sidebarOpened}" class="h-full side-bar"/>
    <!-- /Sidebar -->

    <div class="flex-1 h-full">
      <Navbar @toggle-sidebar="toggleSidebar"></Navbar>
      <!-- Content -->
      <main class="p-6 h-full">
        <router-view></router-view>
      </main>
      <!-- /Content -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import Sidebar from './Sidebar.vue';
import Navbar from './Navbar.vue';

const sidebarOpened = ref(true);

function toggleSidebar() {
  sidebarOpened.value = !sidebarOpened.value;
}

function updateSidebarState() {
  sidebarOpened.value = window.outerWidth > 768;
}

onMounted(() => {
  updateSidebarState();
  window.addEventListener('resize', updateSidebarState);
});

onUnmounted(() => {
  window.removeEventListener('resize', updateSidebarState);
});
</script>

<style scoped>
.side-bar{
    min-height: 100%;
    
}
</style>
