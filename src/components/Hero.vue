<!-- <template>
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
</style> -->
<template>
  <section id="home" class="hero">
    <div class="hero-slideshow">
      <!-- Slides -->
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="slide"
        :class="{ active: index === currentSlide }"
      >
        <div class="hero-image-wrapper">
          <img
            :src="slide.image"
            :alt="slide.alt"
            class="hero-image"
            :style="{ transform: `scale(${slide.scale || 1.5})` }"
          />
          <div class="slide-overlay"></div>
        </div>
      </div>

      <!-- Navigation Dots -->
      <div class="slide-navigation">
        <button
          v-for="(slide, index) in slides"
          :key="`nav-${index}`"
          class="nav-dot"
          :class="{ active: index === currentSlide }"
          @click="goToSlide(index)"
          :aria-label="`Go to slide ${index + 1}`"
        ></button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Hero',
  data() {
    return {
      currentSlide: 0,
      autoplayInterval: null,
      slides: [
        {
          image: '/src/assets/Images/Header Image.jpg',
          alt: 'Luxury Hotel Experience',

          scale: 1.5,
        },
        {
          image: '/src/assets/Images/Header Image.jpg',
          alt: 'Premium Accommodation',

          scale: 1.3,
        },
        {
          image: '/src/assets/Images/Header Image.jpg',
          alt: 'Exceptional Dining',

          scale: 1.4,
        },
        {
          image: '/src/assets/Images/Header Image.jpg',
          alt: 'Relaxation & Wellness',
          scale: 1.6,
        },
      ],
    }
  },
  mounted() {
    this.startAutoplay()
  },
  beforeUnmount() {
    this.stopAutoplay()
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.slides.length
      this.resetAutoplay()
    },
    previousSlide() {
      this.currentSlide = this.currentSlide === 0 ? this.slides.length - 1 : this.currentSlide - 1
      this.resetAutoplay()
    },
    goToSlide(index) {
      this.currentSlide = index
      this.resetAutoplay()
    },
    startAutoplay() {
      this.autoplayInterval = setInterval(() => {
        this.nextSlide()
      }, 5000) // Change slide every 5 seconds
    },
    stopAutoplay() {
      if (this.autoplayInterval) {
        clearInterval(this.autoplayInterval)
        this.autoplayInterval = null
      }
    },
    resetAutoplay() {
      this.stopAutoplay()
      this.startAutoplay()
    },
  },
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

.hero-slideshow {
  position: relative;
  width: 100%;
  height: 100%;
}

.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1s ease-in-out;
  z-index: 1;
}

.slide.active {
  opacity: 1;
  z-index: 2;
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
  transition: transform 8s ease-in-out;
  animation: kenBurns 10s ease-in-out infinite alternate;
}

@keyframes kenBurns {
  0% {
    transform: scale(1.5) translate(0, 0);
  }
  25% {
    transform: scale(1.6) translate(-2%, -1%);
  }
  50% {
    transform: scale(1.7) translate(1%, -2%);
  }
  75% {
    transform: scale(1.6) translate(-1%, 1%);
  }
  100% {
    transform: scale(1.5) translate(0, 0);
  }
}

.slide-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    135deg,
    rgba(0, 0, 0, 0.3) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0.7) 100%
  );
  z-index: 1;
}

/* Slide Content */
.slide-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
  z-index: 3;
  width: 90%;
  max-width: 800px;
}

.slide-text {
  animation: slideInUp 1s ease-out;
}

.slide.active .slide-text {
  animation: slideInUp 1s ease-out;
}

@keyframes slideInUp {
  0% {
    opacity: 0;
    transform: translateY(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.slide-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  margin-bottom: 1rem;
  line-height: 1.2;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
  animation-delay: 0.2s;
}

.slide-subtitle {
  font-size: clamp(1.1rem, 2vw, 1.5rem);
  margin-bottom: 2rem;
  opacity: 0.9;
  line-height: 1.5;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
  animation-delay: 0.4s;
}

.slide-button {
  display: inline-block;
  padding: 1rem 2rem;
  background: linear-gradient(45deg, #007bff, #0056b3);
  color: white;
  text-decoration: none;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-shadow: none;
  box-shadow: 0 4px 15px rgba(0, 123, 255, 0.3);
  animation-delay: 0.6s;
}

.slide-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 123, 255, 0.4);
  background: linear-gradient(45deg, #0056b3, #003d82);
}

/* Navigation Dots */
.slide-navigation {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
  z-index: 4;
}

.nav-dot {
  width: 5px;
  height: 5px;
  border-radius: 50%;
  border: 2px solid rgba(255, 255, 255, 0.5);
  background: transparent;
  cursor: pointer;
  transition: all 0.3s ease;
}

.nav-dot:hover {
  border-color: rgba(255, 255, 255, 0.8);
  transform: scale(1.2);
}

.nav-dot.active {
  background: white;
  border-color: white;
  transform: scale(1.3);
}



@media (max-width: 767px) {
  .slide-content {
    width: 95%;
    padding: 0 1rem;
  }

  .slide-title {
    font-size: clamp(2rem, 8vw, 3rem);
  }

  .slide-subtitle {
    font-size: clamp(1rem, 4vw, 1.3rem);
  }

  .slide-button {
    padding: 0.8rem 1.5rem;
    font-size: 1rem;
  }

  .slide-navigation {
    bottom: 20px;
  }

  .nav-dot {
    width: 6px;
    height: 6px;
  }
}

/* Pause animations on hover */
.hero-slideshow:hover .hero-image {
  animation-play-state: paused;
}
</style>
