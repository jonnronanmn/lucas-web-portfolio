<template>
  <div>
    <!-- Floating Button -->
    <button class="contact-float-btn" @click="isOpen = true">
      <span class="btn-icon">💬</span>
      <span class="btn-text">Contact</span>
    </button>

    <!-- Centered Contact Modal -->
    <div class="contact-modal" v-if="isOpen">
      <div class="contact-container">
        <div class="contact-header d-flex justify-content-between align-items-center">
          <h5>Contact Me</h5>
          <button class="close-btn" @click="isOpen = false">&times;</button>
        </div>

        <form @submit.prevent="handleSubmit">
          <div class="mb-3">
            <label for="nameInput" class="form-label">Full Name</label>
            <input type="text" id="nameInput" v-model="name" placeholder="Your Name" required />
          </div>
          <div class="mb-3">
            <label for="emailInput" class="form-label">Email Address</label>
            <input type="email" id="emailInput" v-model="email" placeholder="Your Email" required />
          </div>
          <div class="mb-3">
            <label for="subjectInput" class="form-label">Subject</label>
            <input type="text" id="subjectInput" v-model="subject" placeholder="Subject" required />
          </div>
          <div class="mb-3">
            <label for="messageInput" class="form-label">Message</label>
            <textarea id="messageInput" rows="4" v-model="message" placeholder="Write your message here" required></textarea>
          </div>
          <button type="submit" class="btn-submit w-100">{{ isLoading ? "Sending..." : "Submit" }}</button>
        </form>
      </div>
      <div class="overlay-bg" @click="isOpen = false"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Notyf } from 'notyf';
import 'notyf/notyf.min.css'

const accessKey = import.meta.env.VITE_WEB3FORMS_ACCESS_KEY

const name = ref("");
const email = ref("");
const message = ref("");
const subject = ref("");
const isLoading = ref(false);
const isOpen = ref(false);

const handleSubmit = async () => {

            // if(!recaptchaToken.value){
            //     notyf.error("Please verify that you are not a robot.");
            //     return;
            // }

            isLoading.value = true;
            try{
                const response = await fetch("https://api.web3forms.com/submit", {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Accept': 'application/json'
                    },
                    body: JSON.stringify({
                        access_key: accessKey,
                        subject: subject.value,
                        name: name.value,
                        email: email.value,
                        message: message.value

                    })
                })
                const result = await response.json();
                if(result.success){
                    console.log(result);
                    isLoading.value = false;
                    notyf.success("Message Sent!");
                }
            }catch(error){
                console.log(error);
                isLoading.value = false;
                notyf.error('Failed to send message.');
            // }finally{
            //     resetRecaptcha();
            }

    }

//         const SITE_KEY = '6Lcj-cYrAAAAAPH-erEm-XETzGdva_Uc-G2p9nYQ';  // Replace with your site key

// const recaptchaContainer = ref(null);
// const recaptchaWidgetId = ref(null);
// const recaptchaToken = ref('');

// // Callback called by reCAPTCHA when successful
// function onRecaptchaSuccess(token) {
//   recaptchaToken.value = token;
// }

// // Callback when expired
// function onRecaptchaExpired() {
//   recaptchaToken.value = '';
// }

// // Function to render the reCAPTCHA widget
// function renderRecaptcha() {
//   if (!window.grecaptcha) {
//     console.error('reCAPTCHA not loaded');
//     return;
//   }

//   recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
//     sitekey: SITE_KEY,
//     size: 'normal', // or 'compact'
//     callback: onRecaptchaSuccess,
//     'expired-callback': onRecaptchaExpired,
//   });
// }

// // Function to reset reCAPTCHA 
// function resetRecaptcha() {
//   if (recaptchaWidgetId.value !== null) {
//     window.grecaptcha.reset(recaptchaWidgetId.value);
//     recaptchaToken.value = '';
//   }
// }



// onMounted(() => {
//   // This code waits for the Google reCAPTCHA library to load, then renders the reCAPTCHA widget using onMounted hook. 
//   // The widget is rendered with grecaptcha.render(), which requires a sitekey. 
//   // Callback functions handle success and expiration events. 
//   // reCAPTCHA is reset upon form submission to clear the token.
//   const interval = setInterval(() => {
//     if (window.grecaptcha && window.grecaptcha.render) {
//       renderRecaptcha();
//       clearInterval(interval);
//     }
//   }, 100);

//   onBeforeUnmount(() => {
//     clearInterval(interval);
//   });
// });
</script>

<style scoped>
/* Floating Button */
.contact-float-btn {
  position: fixed;
  right: 20px;
  bottom: 40px;
  z-index: 999;
  display: flex;
  align-items: center;
  gap: 0.4rem;
  background-color: #0d6efd;
  color: #fff;
  border: none;
  border-radius: 40px;
  padding: 0.5rem 1rem;
  font-weight: 500;
  font-size: 0.85rem;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  transition: all 0.3s ease;
}
.contact-float-btn:hover {
  transform: translateY(-2px) scale(1.05);
  background-color: #0b5ed7;
}

.btn-icon {
  font-size: 1rem;
  animation: wave 2s infinite;
}
@keyframes wave {
  0%, 60%, 100% { transform: rotate(0deg); }
  20% { transform: rotate(15deg); }
  40% { transform: rotate(-15deg); }
}

/* Centered Modal */
.contact-modal {
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 998;
}

/* Background Overlay */
.overlay-bg {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.6);
  cursor: pointer;
}

/* Contact Container */
.contact-container {
  position: relative;
  width: 100%;
  max-width: 400px;
  background-color: #031624;
  border: 1px solid #0d6efd;
  border-radius: 12px;
  padding: 2rem;
  color: #fff;
  z-index: 1;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

/* Header */
.contact-header h5 {
  margin: 0;
  font-weight: bold;
  color: #fff;
  font-size: 1.2rem;
}
.close-btn {
  background: transparent;
  border: none;
  font-size: 1.5rem;
  color: #fff;
  cursor: pointer;
}

/* Form Inputs */
.contact-container input,
.contact-container textarea {
  width: 100%;
  background-color: #0d1b2a;
  border: 1px solid #0d6efd;
  color: #fff;
  padding: 0.5rem 0.7rem;
  border-radius: 6px;
  margin-bottom: 0.9rem;
  font-size: 0.85rem;
  transition: border-color 0.3s ease;
}
.contact-container input::placeholder,
.contact-container textarea::placeholder {
  color: #ccc;
}
.contact-container input:focus,
.contact-container textarea:focus {
  outline: none;
  border-color: #6610f2;
}

/* Submit Button */
.btn-submit {
  background-color: #0d6efd;
  color: #fff;
  font-weight: 500;
  padding: 0.5rem;
  border-radius: 6px;
  border: none;
  font-size: 0.85rem;
  transition: all 0.3s ease;
}
.btn-submit:hover {
  background-color: #6610f2;
  transform: translateY(-2px);
  box-shadow: 0 5px 12px rgba(0,0,0,0.4);
}

/* Responsive */
@media (max-width: 768px) {
  .contact-container {
    width: 90%;
    padding: 1.5rem;
  }
  .contact-float-btn {
    padding: 0.4rem 0.8rem;
    font-size: 0.75rem;
  }
  .btn-icon {
    font-size: 0.9rem;
  }
}
</style>