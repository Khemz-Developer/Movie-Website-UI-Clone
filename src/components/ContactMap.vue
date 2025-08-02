<template> 
  <section id="contact" class="contact-map section">
    <div class="container">
      <h2 class="section-title">How to reach us</h2>
      <p class="contact-subtitle">Lorem ipsum dolor sit amet, consetetur.</p>
      
      <div class="contact-grid">
        <div class="contact-form">
          <form @submit.prevent="submitForm">
            <div class="form-row">
              <div class="form-group">
                <label class="form-label">First Name *</label>
                <input 
                  v-model="form.firstName"
                  type="text" 
                  class="form-input"
                  :class="{ 'error-field': errors.firstName }"
                  @blur="validateField('firstName')"
                />
                <div v-if="errors.firstName" class="error">{{ errors.firstName }}</div>
              </div>
              
              <div class="form-group">
                <label class="form-label">Last Name *</label>
                <input 
                  v-model="form.lastName"
                  type="text" 
                  class="form-input"
                  :class="{ 'error-field': errors.lastName }"
                  @blur="validateField('lastName')"
                />
                <div v-if="errors.lastName" class="error">{{ errors.lastName }}</div>
              </div>
            </div>
            
            <div class="form-group">
              <label class="form-label">Email *</label>
              <input 
                v-model="form.email"
                type="email" 
                class="form-input"
                :class="{ 'error-field': errors.email }"
                @blur="validateField('email')"
              />
              <div v-if="errors.email" class="error">{{ errors.email }}</div>
            </div>
            
            <div class="form-group">
              <label class="form-label">Telephone</label>
              <input 
                v-model="form.telephone"
                type="tel" 
                class="form-input"
              />
            </div>
            
            <div class="form-group">
              <label class="form-label">Message *</label>
              <textarea 
                v-model="form.message"
                class="form-textarea"
                :class="{ 'error-field': errors.message }"
                rows="5"
                @blur="validateField('message')"
              ></textarea>
              <div v-if="errors.message" class="error">{{ errors.message }}</div>
            </div>
            
            <div class="bottom-section">
              <div class="required-note">* required fields</div>
              <div class="form-group checkbox-group">
                <label class="checkbox-label">
                  <input 
                    v-model="form.agreeTerms"
                    type="checkbox" 
                    class="checkbox-input"
                    :class="{ 'error-field': errors.agreeTerms }"
                    @change="validateField('agreeTerms')"
                  />
                  <span class="checkbox-custom"></span>
                  I agree to the <span class="terms-link">Terms & Conditions</span>
                </label>
                <div v-if="errors.agreeTerms" class="error">{{ errors.agreeTerms }}</div>
              </div>
              
              
              
              <button type="submit" class="btn submit-btn">SUBMIT</button>
            </div>
          </form>
        </div>
        
        <div class="map-container">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3037.8944654087596!2d-3.6357109!3d40.4383266!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd42289c5f3ee0cf%3A0x6b69c78e6b5c9e31!2sAmadeus%20IT%20Group%20SA!5e0!3m2!1sen!2sus!4v1635789123456!5m2!1sen!2sus"
            width="100%"
            height="400"
            style="border:0;"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
            title="Amadeus IT Group Location"
          ></iframe>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactMap',
  data() {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        telephone: '',
        message: '',
        agreeTerms: false
      },
      errors: {}
    }
  },
  methods: {
    validateField(fieldName) {
      this.errors = { ...this.errors }
      delete this.errors[fieldName]
      
      switch (fieldName) {
        case 'firstName':
          if (!this.form.firstName.trim()) {
            this.errors.firstName = 'First name is required'
          }
          break
        case 'lastName':
          if (!this.form.lastName.trim()) {
            this.errors.lastName = 'Last name is required'
          }
          break
        case 'email':
          if (!this.form.email.trim()) {
            this.errors.email = 'Email is required'
          } else if (!this.isValidEmail(this.form.email)) {
            this.errors.email = 'Please enter a valid email'
          }
          break
        case 'message':
          if (!this.form.message.trim()) {
            this.errors.message = 'Message is required'
          }
          break
        case 'agreeTerms':
          if (!this.form.agreeTerms) {
            this.errors.agreeTerms = 'You must agree to the terms and conditions'
          }
          break
      }
    },
    
    validateForm() {
      this.errors = {}
      
      this.validateField('firstName')
      this.validateField('lastName')
      this.validateField('email')
      this.validateField('message')
      this.validateField('agreeTerms')
      
      return Object.keys(this.errors).length === 0
    },
    
    isValidEmail(email) {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      return emailRegex.test(email)
    },
    
    submitForm() {
      if (this.validateForm()) {
        // Form is valid - show success message
        const formData = {
          'First Name': this.form.firstName,
          'Last Name': this.form.lastName,
          'Email': this.form.email,
          'Telephone': this.form.telephone || 'Not provided',
          'Message': this.form.message,
          'Agreed to Terms': this.form.agreeTerms ? 'Yes' : 'No'
        }
        
        let message = 'Form submitted successfully!\n\nForm Data:\n'
        for (const [key, value] of Object.entries(formData)) {
          message += `${key}: ${value}\n`
        }
        
        alert(message)
        
        // Reset form
        this.form = {
          firstName: '',
          lastName: '',
          email: '',
          telephone: '',
          message: '',
          agreeTerms: false
        }
        this.errors = {}
      }
    }
  }
}
</script>

<style scoped>
.contact-map {
  background: #1a1a1a;
  color: white;
  padding: 4rem 0;
}

.section-title {
  text-align: left;
  color: #ffffff;
  font-size: 2.5rem;
  font-weight: 400;
  margin-bottom: 1rem;
  letter-spacing: -0.5px;
}

.contact-subtitle {
  text-align: left;
  color: #888;
  margin-bottom: 3rem;
  font-size: 16px;
  line-height: 1.5;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1200px;
  margin: 0 auto;
}

@media (max-width: 767px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  .contact-grid {
    gap: 3rem;
  }
}

.contact-form {
  background: transparent;
  padding: 0;
}

@media (max-width: 767px) {
  .contact-form {
    padding: 0;
  }
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

@media (max-width: 767px) {
  .form-row {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-label {
  display: block;
  color: #fff;
  font-size: 14px;
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 1rem;
  border: 1px solid #555;
  border-radius: 4px;
  font-size: 14px;
  font-family: 'Inter', sans-serif;
  outline: none;
  transition: border-color 0.3s ease;
  background: #333;
  color: #fff;
  box-sizing: border-box;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #888;
  background: #404040;
}

.form-input::placeholder,
.form-textarea::placeholder {
  color: #888;
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
  font-family: inherit;
}

.error-field {
  border-color: #ff4444 !important;
}

.error {
  color: #ff4444;
  font-size: 12px;
  margin-top: 0.25rem;
  line-height: 1.3;
}

.bottom-section {
  margin-top: 2rem;
}

.checkbox-group {
  margin-bottom: 0.5rem;
}

.checkbox-group .checkbox-label {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  cursor: pointer;
  font-size: 14px;
  line-height: 1.4;
  color: #fff;
}

.checkbox-input {
  display: none;
}

.checkbox-input:checked + .checkbox-custom {
  background: #fff;
  border-color: #fff;
}

.checkbox-input:checked + .checkbox-custom::after {
  opacity: 1;
}

.checkbox-input.error-field + .checkbox-custom {
  border-color: #ff4444;
}

.checkbox-custom {
  width: 16px;
  height: 16px;
  border: 1px solid #888;
  border-radius: 2px;
  background: transparent;
  position: relative;
  flex-shrink: 0;
  margin-top: 2px;
  transition: all 0.3s ease;
}

.checkbox-custom::after {
  content: '✓';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #000;
  font-size: 10px;
  font-weight: bold;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.terms-link {
  text-decoration: underline;
  color: #fff;
}

.required-note {
  color: #888;
  font-size: 12px;
  margin-bottom: 1.5rem;
  text-align: left;
}

.submit-btn {
  background: #cc9400;
  padding: 1rem 3rem;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 1px;
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  min-width: 220px;
  display: block;
  margin-left: auto;
}

.submit-btn:hover {
  background: #d6a41a;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(255, 140, 0, 0.3);
}

.map-container {
  border-radius: 4px;
  overflow: hidden;
  height: 100%;
  min-height: 400px;
}

.map-container iframe {
  display: block;
  width: 100%;
  height: 100%;
  min-height: 400px;
  filter: grayscale(20%) contrast(1.1);
}

/* Container and section styles */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 768px) {
  .container {
    padding: 0 1rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .form-row {
    gap: 1rem;
  }
  
  .submit-btn {
    width: auto;             
    min-width: 220px;       
    display: block;          
    margin: 0 auto;         
    padding: 1.25rem;
    margin-top: 30px;
  }
}
</style>