<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <nav class="navbar bg-primary" data-bs-theme="dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">7 Wonders Of The World</a>
    </div>
  </nav>
  <div class="container">
    <RouterView />
  </div>
</template>

<style scoped>

</style>
