<template>
  <section class="introduction section">
    <div class="top-border-line"></div>
    <div class="container">
      <div class="intro-content">
        <h1 class="section-title">MOVIE LIBRARY</h1>
        <p class="intro-text">
          Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor
          invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
        </p>
        <div class="intro-features">
          <div class="feature">
            <h3>Collect your favourites</h3>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Introduction',
}
</script>

<style scoped>
.introduction {
  background: #000000;
  padding: 4rem 0;
  min-height: 400px;
}

@media (max-width: 767px) {
  .introduction {
    padding: 3rem 0;
  }
}

.top-border-line {
  width: 100%;
  height: 1px; /* thickness of the line */
  background-color: rgb(107, 106, 106);
  margin-bottom: 2rem; /* space below the line before the heading */
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.intro-content {
  max-width: 800px;
  margin-left: 0;
  padding-left: 0rem;
  text-align: left;
  padding-top: 2rem;
}

.section-title {
  color: #ffffff; /* White text */
  font-size: 4rem; /* Larger, bolder title */
  font-weight: 500;
  letter-spacing: 2px;
  margin-bottom: 2rem;
  line-height: 1.2;
}

@media (max-width: 767px) {
  .section-title {
    font-size: 2.5rem;
    letter-spacing: 1px;
  }
}

.intro-text {
  font-size: 16px;
  line-height: 1.6;
  color: #cccccc; /* Light gray text for better readability */
  margin-bottom: 3rem;
  max-width: 600px; /* Constrain width for better readability */
}

@media (max-width: 767px) {
  .intro-text {
    font-size: 14px;
    margin-bottom: 2rem;
  }
}

.intro-features {
  margin-top: 3rem;
}

.feature h3 {
  font-size: 18px;
  font-weight: 400;
  color: #ffffff;
  margin-bottom: 1.5rem;
  letter-spacing: 0.5px;
}

@media (max-width: 767px) {
  .feature h3 {
    font-size: 16px;
  }
}

/* Add some subtle styling enhancements */
.introduction::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(0, 0, 0, 1) 0%, rgba(20, 20, 20, 1) 100%);
  z-index: -1;
}

.introduction {
  position: relative;
}
</style>
