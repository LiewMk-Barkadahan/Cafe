<script setup>
import { ref, watch } from 'vue'
import { useRoute } from 'vue-router'
import { Icon } from '@iconify/vue'

const isOpen = ref(false)
const route = useRoute()

watch(() => route.path, () => {
  isOpen.value = false
})

function toggleMenu() {
  isOpen.value = !isOpen.value
}

function closeMenu() {
  isOpen.value = false
}
</script>

<template>
  <nav class="navbar">
    <div class="navbar-inner glass">
      <router-link to="/" class="brand">
        <Icon icon="mdi:coffee" width="20" height="20" class="brand-icon" />
        <span class="brand-text">LiewMk</span>
      </router-link>

      <button
        class="menu-toggle"
        @click="toggleMenu"
        :class="{ active: isOpen }"
        :aria-label="isOpen ? 'Close menu' : 'Open menu'"
        :aria-expanded="isOpen"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>

      <div class="nav-links" :class="{ open: isOpen }">
        <router-link to="/" class="nav-link" @click="closeMenu">Home</router-link>
        <router-link to="/menu" class="nav-link" @click="closeMenu">Menu</router-link>
      </div>
    </div>

    <!-- Mobile backdrop -->
    <Transition name="fade">
      <div v-if="isOpen" class="backdrop" @click="closeMenu"></div>
    </Transition>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  pointer-events: none;
}

.navbar-inner {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 1.25rem;
  max-width: 560px;
  margin: 0.75rem auto 0;
  width: min(92%, 560px);
  pointer-events: auto;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-weight: 800;
  font-size: 1.05rem;
  color: var(--primary-color);
  letter-spacing: -0.3px;
}

.brand-icon {
  color: var(--primary-color);
}

.nav-links {
  display: flex;
  gap: 0.2rem;
}

.nav-link {
  padding: 0.35rem 0.9rem;
  border-radius: 20px;
  font-size: 0.82rem;
  font-weight: 500;
  color: var(--text-mid);
  transition: all 0.25s cubic-bezier(0.22, 1, 0.36, 1);
}

.nav-link:hover {
  color: var(--primary-color);
  background: rgba(93, 64, 55, 0.06);
}

.nav-link.router-link-exact-active {
  background: var(--primary-color);
  color: white;
  box-shadow: 0 2px 8px rgba(93, 64, 55, 0.3);
}

/* Hamburger */
.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 6px;
}

.menu-toggle span {
  width: 18px;
  height: 2px;
  background: var(--text-dark);
  border-radius: 2px;
  transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
  transform-origin: center;
}

.menu-toggle.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.menu-toggle.active span:nth-child(2) {
  opacity: 0;
  transform: scaleX(0);
}

.menu-toggle.active span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

/* Backdrop */
.backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: -1;
  pointer-events: auto;
}

/* Mobile */
@media (max-width: 500px) {
  .menu-toggle {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: calc(100% + 6px);
    left: 0;
    right: 0;
    flex-direction: column;
    background: rgba(255, 255, 255, 0.97);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-radius: var(--radius-lg);
    padding: 0.5rem;
    box-shadow: var(--shadow-lg);
    border: 1px solid rgba(255, 255, 255, 0.6);
    opacity: 0;
    pointer-events: none;
    transform: translateY(-6px);
    transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
  }

  .nav-links.open {
    opacity: 1;
    pointer-events: auto;
    transform: translateY(0);
  }

  .nav-link {
    text-align: center;
    padding: 0.6rem 1rem;
    border-radius: var(--radius-md);
  }
}

/* Fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
