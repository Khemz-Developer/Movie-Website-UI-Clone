
<template>
  <header class="header">
    <div class="container">
      <nav class="navbar">
        <div class="navbar-brand">
          <img src="/src/assets/Logos/Logo White.svg" alt="Logo" class="logo" />
        </div>
        <ul class="navbar-nav" :class="{ active: mobileMenuOpen }">
          <li class="nav-item">
            <a href="#home" class="nav-link" @click="closeMenu">HOME</a>
          </li>
          <li class="nav-item">
            <a href="#screens" class="nav-link" @click="closeMenu">OUR SCREENS</a>
          </li>
          <li class="nav-item">
            <a href="#schedule" class="nav-link" @click="closeMenu">SCHEDULE</a>
          </li>
          <li class="nav-item">
            <a
              href="#library"
              class="nav-link"
              @click="closeMenu"
              style="border-bottom: 2px solid #ffd700"
              >MOVIE LIBRARY</a
            >
          </li>
          <li class="nav-item">
            <a href="#contact" class="nav-link" @click="closeMenu">LOCATION & CONTACT</a>
          </li>
        </ul>

        <button class="hamburger" @click="toggleMenu" :class="{ active: mobileMenuOpen }">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      mobileMenuOpen: false,
    }
  },
  methods: {
    toggleMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen
    },
    closeMenu() {
      this.mobileMenuOpen = false
    },
  },
}
</script>

<style scoped>
.header {
  background: #000000;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
  min-height: 70px;
}

.navbar-nav {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
}

@media (max-width: 768px) {
  .navbar-nav {
    position: fixed;
    top: 70px;
    left: -100%;
    width: 100%;
    height: calc(100vh - 70px);
    background: #000000;
    flex-direction: column;
    padding: 2rem;
    transition: left 0.3s ease;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  }

  .navbar-nav.active {
    left: 0;
  }
}

@media (max-width: 1024px) {
  .navbar-nav {
    gap: 1.5rem;
  }
}

.nav-item .nav-link {
  text-decoration: none;
  color: #ffffff;
  font-weight: 500;
  font-size: 0.875rem;
  letter-spacing: 0.5px;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: all 0.3s ease;
  text-transform: uppercase;
  position: relative;
}

.nav-item .nav-link:hover {
  color: #ffd700;
}

@media (max-width: 768px) {
  .nav-item .nav-link {
    font-size: 1rem;
    padding: 1rem;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    display: block;
    width: 100%;
  }
}

.hamburger {
  display: none;
  flex-direction: column;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
}

.hamburger span {
  width: 25px;
  height: 3px;
  background: #ffffff;
  margin: 2px 0;
  transition: all 0.3s ease;
  border-radius: 2px;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -6px);
}
</style>
