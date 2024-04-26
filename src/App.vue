<script setup>
import { RouterView } from 'vue-router'
import Navbar from "@/components/Navbar.vue";
</script>

<template>
  <div class="d-flex flex-column h-100">
    <main class="flex-shrink-0">
      <Navbar/>
      <RouterView />
    </main>
  </div>
</template>