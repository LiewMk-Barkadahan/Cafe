<script setup>
import NavBar from './components/NavBar.vue'
</script>

<template>
  <NavBar />
  <router-view v-slot="{ Component }">
    <transition name="page" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
</template>
