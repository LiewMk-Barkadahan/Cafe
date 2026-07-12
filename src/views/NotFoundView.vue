<script setup>
import { Icon } from '@iconify/vue'
</script>

<template>
  <div class="not-found">
    <div class="content animate-fade-in">
      <Icon icon="mdi:coffee-off" width="64" height="64" class="icon" />
      <h1>404</h1>
      <p>Looks like this page doesn't exist.</p>
      <router-link to="/" class="back-btn">
        <Icon icon="mdi:home" width="18" height="18" />
        <span>Back to Home</span>
      </router-link>
    </div>
  </div>
</template>

<style scoped>
.not-found {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 2rem;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.icon {
  color: var(--text-muted);
  opacity: 0.5;
}

h1 {
  font-size: 4rem;
  font-weight: 800;
  color: var(--primary-color);
  line-height: 1;
}

p {
  color: var(--text-muted);
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

.back-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.7rem 1.4rem;
  font-size: 0.9rem;
  font-weight: 600;
  color: white;
  background: var(--primary-color);
  border-radius: 24px;
  text-decoration: none;
  transition: all 0.25s cubic-bezier(0.22, 1, 0.36, 1);
}

.back-btn:hover {
  background: var(--primary-light);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(93, 64, 55, 0.3);
}
</style>
