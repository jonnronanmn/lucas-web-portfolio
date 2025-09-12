<template>
  <section id="projects" class="projects-section py-5">
    <div class="container">
      <!-- Heading -->
      <div class="text-center mb-5">
        <h2 class="fw-bold text-uppercase text-white">My Projects</h2>
        <p class="section-subtitle">
          A curated showcase of apps, APIs, and designs I’ve built
        </p>
      </div>

      <!-- Projects Grid with Timeline Line -->
      <div class="projects-grid">
        <div
          v-for="(chunk, chunkIndex) in chunkedProjects"
          :key="chunkIndex"
          class="projects-row"
        >
          <div
            v-for="(project, index) in chunk"
            :key="project.id"
            class="project-card-wrapper"
            :class="{ 'timeline-left': index % 2 === 0, 'timeline-right': index % 2 !== 0 }"
          >
            <div class="project-card">
              <div class="project-image">
                <img :src="project.image" :alt="project.title" />
                <div class="overlay">
                  <a :href="project.link" target="_blank" class="btn project-btn">
                    View Project →
                  </a>
                </div>
              </div>
              <div class="project-content">
                <h5 class="fw-bold text-white">{{ project.title }}</h5>
                <p class="project-desc">{{ project.description }}</p>
                <div class="d-flex flex-wrap gap-2 mt-2">
                  <span
                    v-for="tag in project.tags || []"
                    :key="tag"
                    class="badge tech-badge"
                  >
                    {{ tag }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Center line -->
      <div class="timeline-line"></div>
    </div>
  </section>
</template>

<script setup>
import { computed } from "vue";
import projects from "../data/products.json";

const chunkSize = 2; // 2 projects per row

const chunkedProjects = computed(() => {
  const chunks = [];
  for (let i = 0; i < projects.length; i += chunkSize) {
    chunks.push(projects.slice(i, i + chunkSize));
  }
  return chunks;
});
</script>

<style scoped>
.projects-section {
  background-color: #031624;
  position: relative;
}

.section-subtitle {
  color: #ffffffcc;
  font-size: 1rem;
}

/* Timeline Line */
.timeline-line {
  position: absolute;
  top: 140px;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  background: linear-gradient(180deg, #0d6efd, transparent);
  z-index: 0;
}

/* Projects Grid */
.projects-grid {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.projects-row {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
  position: relative;
  z-index: 1;
}

.project-card-wrapper {
  flex: 1 1 40%;
  max-width: 40%;
  perspective: 1000px;
}

/* Optional positioning for left/right cards */
.timeline-left {
  margin-right: 20px;
}
.timeline-right {
  margin-left: 20px;
}

/* Project Card */
.project-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  overflow: hidden;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  transition: transform 0.4s ease, box-shadow 0.4s ease;
}

.project-card:hover {
  transform: translateY(-6px) rotateY(3deg) scale(1.03);
  box-shadow: 0 20px 35px rgba(13, 110, 253, 0.3);
}

/* Image + Overlay */
.project-image {
  position: relative;
  overflow: hidden;
  max-height: 200px;
  border-radius: 12px 12px 0 0;
}

.project-image img {
  width: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.project-card:hover img {
  transform: scale(1.1);
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(3, 22, 36, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transition: opacity 0.4s ease;
}

.project-card:hover .overlay {
  opacity: 1;
}

/* Content */
.project-content {
  padding: 1rem;
}

.project-desc {
  color: #dcdcdc;
  font-size: 0.85rem;
  margin-bottom: 0.5rem;
}

/* Tags */
.tech-badge {
  background: rgba(13, 110, 253, 0.2);
  color: #0d6efd;
  border: 1px solid #0d6efd;
  font-size: 0.75rem;
  padding: 0.25rem 0.5rem;
  border-radius: 20px;
}

/* Button */
.project-btn {
  background-color: #0d6efd;
  color: #fff;
  border: none;
  border-radius: 25px;
  padding: 0.4rem 1rem;
  font-size: 0.85rem;
  transition: all 0.3s ease;
}

.project-btn:hover {
  background-color: #fff;
  color: #0d6efd;
  transform: translateY(-2px);
}

/* Responsive */
@media (max-width: 768px) {
  .project-card-wrapper {
    flex: 1 1 100%;
    max-width: 100%;
    margin: 0 !important;
  }
  .timeline-line {
    left: 8px;
  }
}
</style>