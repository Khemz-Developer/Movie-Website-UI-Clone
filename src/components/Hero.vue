<template>
  <section id="home" class="hero">
    <div class="hero-image-wrapper">
      <img src="/src/assets/Images/Header Image.jpg" alt="Hero Image" class="hero-image" />
      <div class="slide-overlay"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Hero',
}
</script>

<style scoped>
.hero {
  position: relative;
  height: 100vh;
  min-height: 600px;
  overflow: hidden;
  margin-top: 70px;
}

@media (max-width: 767px) {
  .hero {
    height: 70vh;
    min-height: 500px;
  }
}

.hero-image-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 70%;
  transform: scale(1.5); /* ✅ Adjust this value for more/less zoom */
  transition: transform 0.5s ease-in-out;
}

.slide-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.6));
}
</style>
