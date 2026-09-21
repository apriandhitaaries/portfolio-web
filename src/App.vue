<script setup>
import NavBar from './components/AppNavbar.vue'
</script>

<template>
  <div class="min-h-screen bg-white font-sans">
    <NavBar />

    <router-view />
  </div>
</template>
