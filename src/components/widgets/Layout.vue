<script setup lang="ts">
import Header from './Header.vue';

</script>

<template>
  <div class="layout-default w-screen sm:min-h-dvh">
    <Header />
    <main class="container mx-auto px-4 pb-4">
      <slot></slot>
    </main>
  </div>
</template>

<style>
.layout-default {
  background: url(@/assets/images/bg.webp) no-repeat center/cover;
}
</style>