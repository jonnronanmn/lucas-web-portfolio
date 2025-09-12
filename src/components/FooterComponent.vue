<template>
  <footer class="footer-section text-white py-5">
    <div class="container text-center position-relative">
      
      <!-- Horizontal lines with social icons -->
      <div class="d-flex align-items-center justify-content-center mb-3">
        <hr class="flex-grow-1 border-theme" />

        <div class="mx-3 d-flex gap-3">
          <a href="https://github.com/jonnronanmn" target="_blank" rel="noopener" title="GitHub">
            <img src="https://github.githubassets.com/assets/GitHub-Mark-ea2971cee799.png" width="30" height="30" alt="GitHub" />
          </a>
          <a href="https://gitlab.com/jonnronanmn" target="_blank" rel="noopener" title="GitLab">
            <img src="https://yt3.googleusercontent.com/Zfx2OSI5XWKhnove-HwdTokQUmCB7cfpX0uGbqxMeQVNMzVPrvgMadFHpbfYoy04NrjFEBk_3A=s900-c-k-c0x00ffffff-no-rj" width="30" height="30" alt="GitLab" />
          </a>
          <a href="https://www.linkedin.com/in/jonn-l-b0b2161b4/" target="_blank" rel="noopener" title="LinkedIn">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/81/LinkedIn_icon.svg/2048px-LinkedIn_icon.svg.png" width="30" height="30" alt="LinkedIn" />
          </a>
          <a href="https://ron-4043284.postman.co/me" target="_blank" rel="noopener" title="Postman">
            <img src="https://w7.pngwing.com/pngs/28/245/png-transparent-postman-hd-logo.png" width="30" height="30" alt="Postman" />
          </a>
        </div>

        <hr class="flex-grow-1 border-theme" />
      </div>

      <p class="mb-0">&copy; 2025 Jonn Ronan Lucas. All Rights Reserved.</p>
    </div>
  </footer>
</template>

<script setup>
// No additional logic needed
</script>

<style scoped>
.footer-section {
  background-color: #031624; /* Theme background color */
  position: relative;
}

/* Icon hover effects */
.footer-section a img {
  transition: transform 0.3s ease, filter 0.3s ease;
}

.footer-section a img:hover {
  transform: scale(1.2);
  filter: brightness(1.3);
}

/* Horizontal line styling */
hr.border-theme {
  border-color: rgba(255, 255, 255, 0.3); /* Slightly lighter than theme */
  border-width: 1px;
  margin: 0;
}
</style>