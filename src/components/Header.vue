<template>
  <header class="header">
    <div class="container">
      <nav class="navbar">
        <div class="navbar-brand">
          <img src="/src/assets/Logos/Logo White.svg" alt="Logo" class="logo" />
        </div>

        <ul class="nav-menu" :class="{ 'show': mobileMenuOpen }">
          <li>
            <a
              href="#home"
              class="nav-link"
              :class="{ active: activeSection === 'home' }"
              @click="closeMenu"
            >HOME</a>
          </li>
          <li>
            <a
              href="#introduction"
              class="nav-link"
              :class="{ active: activeSection === 'introduction' }"
              @click="closeMenu"
            >OUR SCREENS</a>
          </li>
          <li>
            <a
              href="#schedule"
              class="nav-link"
              :class="{ active: activeSection === 'schedule' }"
              @click="closeMenu"
            >SCHEDULE</a>
          </li>
          <li>
            <a
              href="#library"
              class="nav-link"
              :class="{ active: activeSection === 'library' }"
              @click="closeMenu"
            >MOVIE LIBRARY</a>
          </li>
          <li>
            <a
              href="#contact"
              class="nav-link"
              :class="{ active: activeSection === 'contact' }"
              @click="closeMenu"
            >LOCATION & CONTACT</a>
          </li>
        </ul>

        <div class="menu-toggle" @click="toggleMenu" :class="{ 'menu-open': mobileMenuOpen }">
          <span class="bar bar1"></span>
          <span class="bar bar2"></span>
          <span class="bar bar3"></span>
        </div>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      mobileMenuOpen: false,
      activeSection: "",
    };
  },
  methods: {
    toggleMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen;
    },
    closeMenu() {
      this.mobileMenuOpen = false;
    },
    handleScroll() {
      const sections = ["home", "introduction", "schedule", "library", "contact"];
      for (const id of sections) {
        const section = document.getElementById(id);
        if (section) {
          const rect = section.getBoundingClientRect();
          if (rect.top <= 100 && rect.bottom >= 100) {
            this.activeSection = id;
            break;
          }
        }
      }
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    this.handleScroll(); // Set initial active section
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
};
</script>

<style scoped>
.header {
  background-color: #000;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1000;
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 1rem;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  height: 40px;
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-link {
  color: white;
  text-decoration: none;
  padding-bottom: 0.25rem;
  transition: border-bottom 0.3s ease;
  font-size: 1rem;
}

.nav-link:hover {
  border-bottom: 2px solid #ffd700;
}

.nav-link.active {
  border-bottom: 2px solid #ffd700;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
  width: 30px;
  height: 25px;
  justify-content: space-between;
  position: relative;
}

.bar {
  width: 25px;
  height: 3px;
  background-color: white;
  transition: all 0.3s ease;
  transform-origin: center;
}

/* Hamburger to X animation */
.menu-toggle.menu-open .bar1 {
  transform: rotate(45deg) translate(6px, 6px);
}

.menu-toggle.menu-open .bar2 {
  opacity: 0;
  transform: scale(0);
}

.menu-toggle.menu-open .bar3 {
  transform: rotate(-45deg) translate(6px, -6px);
}

/* Mobile and Tablet Styles (≤1024px) */
@media (max-width: 1024px) {
  .nav-menu {
    display: none;
    flex-direction: column;
    position: absolute;
    right: 1rem;
    top: 100%;
    background: #111;
    padding: 1rem;
    border-radius: 6px;
    width: 200px;
    gap: 1rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
    animation: slideDown 0.3s ease;
  }

  .nav-menu.show {
    display: flex;
  }

  .menu-toggle {
    display: flex;
  }

  .nav-link {
    font-size: 1rem;
  }
}

/* Slide down animation for mobile menu */
@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Optional: Larger font for big screens */
@media (min-width: 1025px) {
  .nav-link {
    font-size: 1.1rem;
  }
}
</style>