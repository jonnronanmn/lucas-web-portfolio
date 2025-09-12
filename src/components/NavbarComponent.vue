<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-dark navbar-custom">
      <div class="container-fluid">
        <!-- Brand -->
        <a class="navbar-brand" href="#landing">JRL</a>

        <!-- Hamburger -->
        <button
          class="navbar-toggler"
          type="button"
          @click="isOpen = !isOpen"
          aria-controls="navbarNav"
          :aria-expanded="isOpen.toString()"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <!-- Navbar links -->
        <div class="collapse navbar-collapse" :class="{ show: isOpen }" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <a class="nav-link" href="#landing" @click="closeMenu">Landing</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#projects" @click="closeMenu">My Projects</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#tools" @click="closeMenu">Tools</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref } from "vue";

const isOpen = ref(false);

const closeMenu = () => {
  isOpen.value = false;
};
</script>

<style scoped>
.navbar-custom {
  background-color: #031624; /* keep dark color */
  padding: 0.5rem 1rem;
  font-size: 1rem;
  position: sticky;
  top: 0;
  z-index: 999;
  box-shadow: 0 4px 6px rgba(255, 255, 255, 0.1); /* subtle light shadow to separate from content */
  border-bottom: 1px solid rgba(255, 255, 255, 0.1); /* subtle border for visibility */
}

.navbar-brand {
  color: #ffffff;
  font-weight: bold;
  font-size: 1.25rem;
  cursor: pointer;
}

.navbar-brand:hover {
  color: #0d6efd;
}

.navbar-nav .nav-link {
  color: #ffffff;
  margin-left: 1rem;
  transition: all 0.3s ease;
}

.navbar-nav .nav-link:hover {
  color: #0d6efd;
}

.navbar-toggler {
  border-color: #ffffff;
}

.navbar-toggler-icon {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3E%3Cpath stroke='rgba(255,255,255,1)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 7h22M4 15h22M4 23h22'/%3E%3C/svg%3E");
}

html {
  scroll-behavior: smooth;
}

@media (max-width: 768px) {
  .navbar-nav {
    margin-top: 1rem;
  }
  .nav-link {
    margin-left: 0;
    margin-bottom: 0.5rem;
  }
}
</style>