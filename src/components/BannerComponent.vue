<template>
  <section id="landing" class="hero-banner">
    <!-- Overlay for contrast -->
    <div class="overlay"></div>

    <!-- Hero Content -->
    <div class="hero-content text-center">
      <!-- Profile Image on top -->
      <div class="hero-image">
        <img 
          src="https://media.licdn.com/dms/image/v2/C5603AQEbgkv2lvQf9g/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1603241852300?e=1760572800&v=beta&t=OWiS8Du27spdvkNtMbu2BLcFbQnjzWjXwiHoI6vIUCc" 
          alt="Profile" 
        />
      </div>

      <h1 class="hero-title mt-4">Hi, I'm Jonn Ronan</h1>
      <h2 class="hero-position">Full Stack Web Developer</h2>
      <p class="hero-paragraph">
   I transitioned from technical recruitment to web development, leveraging my understanding of the tech industry and practical full-stack development experience. I focus on creating clean, user-focused digital solutions, applying problem-solving skills and development know-how to build projects that are both efficient and engaging.
      </p>
    </div>
  </section>
</template>

<script setup>
// No JS needed
</script>

<style scoped>
.hero-banner {
  position: relative;
  background-image: url('https://static.vecteezy.com/system/resources/previews/010/520/048/non_2x/programming-code-background-vector.jpg'); /* professional code wallpaper */
  background-size: cover;
  background-position: center;
  min-height: 95vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  color: #fff;
}

/* Overlay */
.overlay {
  position: absolute;
  inset: 0;
  background-color: rgba(3, 22, 36, 0.65);
  z-index: 0;
}

/* Hero content */
.hero-content {
  position: relative;
  z-index: 1;
  max-width: 650px;
}

/* Profile Image */
.hero-image {
  animation: fadeIn 1s ease forwards;
  opacity: 0;
}
.hero-image img {
  width: 250px;   /* Increased size */
  height: 250px;  /* Increased size */
  border-radius: 50%;
  border: 4px solid #fff;
  object-fit: cover;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.hero-image img:hover {
  transform: scale(1.08); /* Slightly bigger on hover */
  box-shadow: 0 15px 30px rgba(0,0,0,0.6);
}

/* Title */
.hero-title {
  font-size: 3rem;
  font-weight: 700;
  margin-top: 1rem;
  margin-bottom: 1rem;
  animation: fadeInDown 1s ease 0.5s forwards;
}


.hero-position {
  font-size: 2rem;
  font-weight: 550;
  margin-top: 1rem;
  margin-bottom: 1rem;
  animation: fadeInDown 1s ease 0.8s forwards;
}


/* Paragraph */
.hero-paragraph {
  font-size: 1.2rem;
  line-height: 1.6;
  opacity: 0.95;
  margin-bottom: 2rem;
  animation: fadeInUp 1s ease 1s forwards;
}

/* Button */
.btn-hover {
  padding: 0.7rem 2rem;
  border-radius: 30px;
  font-weight: bold;
  background-color: #0d6efd;
  color: #fff;
  text-decoration: none;
  transition: all 0.3s ease;
  display: inline-block;
}
.btn-hover:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(13, 110, 253, 0.5);
}

/* Animations */
@keyframes fadeInDown {
  from { transform: translateY(-20px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}
@keyframes fadeInUp {
  from { transform: translateY(20px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}
@keyframes fadeIn {
  to { opacity: 1; }
}

/* Responsive */
@media(max-width:768px) {
  .hero-title { font-size: 2rem; }
  .hero-paragraph { font-size: 1rem; }
  .hero-image img { width: 150px; height: 150px; } /* Adjusted for smaller screens */
}
</style>