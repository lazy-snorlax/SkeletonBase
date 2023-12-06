<template>
  <div class="auth container-fluid">
    <Suspense>
      <RouterView />
    </Suspense>
  </div>  
</template>

<script lang="ts" setup>
  import { ref, onMounted, onUnmounted } from 'vue'
  import Sidebar from '../components/app/Sidebar.vue'  
</script>