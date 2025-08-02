<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-info">
          <h3 class="footer-title">Amadeus IT Group</h3>
          <address class="footer-address">
            C. Salvador de Madariaga, 1<br>
            28027 Madrid<br>
            Spain
          </address>
        </div>
        
        <div class="footer-social">
          <span class="social-title">Follow us on</span>
          <div class="social-icons">
            <a href="#" class="social-link" aria-label="Twitter">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/>
              </svg>
            </a>
            <a href="#" class="social-link" aria-label="YouTube">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
              </svg>
            </a>
          </div>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p class="copyright">
          Copyright © {{ currentYear }} Amadeus Hotels. All rights reserved.
        </p>
        <p class="credits">
          Photos by <a href="#" class="credit-link">Felix Mooneeram</a> & <a href="#" class="credit-link">Serge Kutuzov</a> on <a href="#" class="credit-link">Unsplash</a>
        </p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.footer {
  background: #111111;
  color: #ffffff;
  padding: 3rem 0 1.5rem;
}

.container {
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 2rem;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 2rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

@media (max-width: 767px) {
  .footer-content {
    flex-direction: column;
    gap: 1.5rem;
    text-align: center;
    align-items: center;
  }
}

.footer-info .footer-title {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #ffffff;
}

.footer-info .footer-address {
  font-style: normal;
  line-height: 1.5;
  color: rgba(255, 255, 255, 0.7);
  font-size: 14px;
}

.footer-social {
  display: flex;
  align-items: center;
  gap: 1rem;
}

@media (max-width: 767px) {
  .footer-social {
    flex-direction: column;
    gap: 1rem;
    justify-content: center;
    align-items: center;
  }
}

.footer-social .social-title {
  font-size: 14px;
  color: rgba(255, 255, 255, 0.7);
  margin-right: 0.5rem;
}

@media (max-width: 767px) {
  .footer-social .social-title {
    margin-right: 0;
    margin-bottom: 0;
  }
}

.footer-social .social-icons {
  display: flex;
  gap: 0.75rem;
  justify-content: center;
}

.footer-social .social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-social .social-link:hover {
  color: #ffffff;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 12px;
  color: rgba(255, 255, 255, 0.5);
}

@media (max-width: 767px) {
  .footer-bottom {
    flex-direction: column;
    gap: 0.75rem;
    text-align: center;
  }
}

.copyright,
.credits {
  margin: 0;
}

.credit-link {
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
}

.credit-link:hover {
  color: #ffffff;
  text-decoration: underline;
}
</style>