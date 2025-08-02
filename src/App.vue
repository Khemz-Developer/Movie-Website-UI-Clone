<template>
  <div id="app">
    <Header />
    <Hero />
    <Introduction />
    <MovieGrid />
    <ContactMap />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Introduction from './components/Introduction.vue'
import MovieGrid from './components/MovieGrid.vue'
import ContactMap from './components/ContactMap.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Hero,
    Introduction,
    MovieGrid,
    ContactMap,
    Footer
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', sans-serif;
  line-height: 1.6;
  color: #333;
}

html {
  scroll-behavior: smooth;
}
</style>