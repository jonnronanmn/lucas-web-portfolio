<template>
  <section id="tools" class="tools-section py-5">
    <div class="container">
      <!-- Heading -->
      <div class="text-center mb-5">
        <h2 class="fw-bold text-uppercase text-white">Tech Stack</h2>
        <p class="section-subtitle">A showcase of the technologies I work with</p>
      </div>

      <!-- Category Tabs -->
      <div class="d-flex justify-content-center gap-3 mb-4 flex-wrap">
        <button 
          v-for="category in categories" 
          :key="category" 
          class="tab-btn"
          :class="{ active: activeCategory === category }"
          @click="activeCategory = category"
        >
          {{ category }}
        </button>
      </div>

      <!-- Tools Grid -->
      <div class="row g-4 justify-content-center">
        <div 
          v-for="tool in filteredTools" 
          :key="tool.id" 
          class="col-6 col-md-4 col-lg-3"
        >
          <div class="glass-card text-center">
            <div class="logo-wrapper">
              <img :src="tool.logo" :alt="tool.name" />
            </div>
            <h6 class="mt-3 text-white">{{ tool.name }}</h6>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import tools from "../data/tools.json"; // <-- Import your JSON file

// Define categories
const categories = ["Frontend", "Backend", "Full Stack", "Other"];
const activeCategory = ref("Frontend");

// Compute filtered tools based on active category
const filteredTools = computed(() => 
  tools.filter(tool => tool.category === activeCategory.value)
);
</script>

<style scoped>
.tools-section {
  padding-top: 4rem;
  padding-bottom: 4rem;
  background-color: #031624;
}

.section-subtitle {
  color: #ffffffcc;
}

/* Tabs */
.tab-btn {
  background: transparent;
  border: 1px solid #ffffff33;
  color: #fff;
  padding: 0.5rem 1.2rem;
  border-radius: 30px;
  font-size: 0.9rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.tab-btn:hover {
  background: #0d6efd44;
  border-color: #0d6efd;
}

.tab-btn.active {
  background: #0d6efd;
  border-color: #0d6efd;
  font-weight: bold;
}

/* Glass cards */
.glass-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 1.5rem 1rem;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.glass-card:hover {
  transform: translateY(-6px) scale(1.05);
  box-shadow: 0 15px 30px rgba(0, 123, 255, 0.3);
}

.logo-wrapper img {
  width: 60px;
  height: 60px;
  object-fit: contain;
  transition: transform 0.3s ease;
}

.glass-card:hover .logo-wrapper img {
  transform: rotate(5deg) scale(1.1);
}
</style>