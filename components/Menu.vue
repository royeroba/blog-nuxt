<template>
  <nav class="navbar">
    <div class="navbar-content">
      <div class="logo">
        <NuxtLink
          :to="{ name: 'index' }"
          class="nav-button"
          active-class="active"
        >
          Blog Gamer and Sports
        </NuxtLink>
      </div>

      <div class="hamburger" @click="toggleMenu">
        <div class="line"></div>
        <div class="line"></div>
        <div class="line"></div>
      </div>

      <div :class="['nav-links', { 'nav-active': menuOpen }]">
        <NuxtLink
          :to="{ name: 'blog' }"
          class="nav-button"
          active-class="active"
          >Blog</NuxtLink
        >
        <NuxtLink
          :to="{ name: 'contact' }"
          class="nav-button"
          active-class="active"
          >Contact</NuxtLink
        >
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

const menuOpen = ref(false);

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};
</script>

<style scoped>
.navbar {
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: white;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.navbar-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px 20px;
}

.logo img {
  height: 40px;
}

.nav-links {
  display: flex;
  gap: 20px;
}

.nav-button {
  color: #333;
  text-decoration: none;
  padding: 10px 15px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
  font-size: 1.2rem;
}

.active {
  border-bottom: 2px solid #0056b3;
}

.nav-button:hover {
  background-color: #f0f0f0;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
  gap: 5px;
}

.hamburger .line {
  width: 25px;
  height: 3px;
  background-color: #333;
}

@media (max-width: 768px) {
  .nav-links {
    position: absolute;
    top: 60px;
    right: 0;
    background-color: white;
    flex-direction: column;
    width: 100%;
    height: 0;
    overflow: hidden;
    transition: height 0.3s ease;
    border-top: 1px solid #ddd;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  }

  .nav-active {
    height: 150px;
  }

  .nav-button {
    padding: 15px;
    font-size: 1.5rem;
    text-align: center;
  }

  .hamburger {
    display: flex;
  }
}

@media (max-width: 480px) {
  .navbar-content {
    padding: 10px;
  }

  .logo {
    font-size: 1rem;
  }

  .nav-button {
    font-size: 1.2rem;
  }
}
</style>
