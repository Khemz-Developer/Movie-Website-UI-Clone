<template>
  <Header />
  <Hero />
  <Introduction />
  <MovieGrid />
  <ContactMap />
  <Footer />
</template>

<script>
import Header from '../components/Header.vue'
import Hero from '../components/Hero.vue'
import Introduction from '../components/Introduction.vue'
import MovieGrid from '../components/MovieGrid.vue'
import ContactMap from '../components/ContactMap.vue'
import Footer from '../components/Footer.vue'

export default {
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
