<template>
  <div>
    <!-- Floating Button -->
    <button class="contact-float-btn" @click="isOpen = true">
      <span class="btn-icon">📩</span>
      <span class="btn-text">Contact Me</span>
    </button>

    <!-- Centered Contact Modal -->
    <div class="contact-modal" v-if="isOpen">
      <div class="overlay-bg" @click="isOpen = false"></div>
      <div class="contact-container show">
        <div class="contact-header">
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
            <textarea id="messageInput" rows="4" v-model="message" placeholder="Write your message here"
              required></textarea>
          </div>

          <!-- reCAPTCHA -->
          <div ref="recaptchaContainer" class="mb-3 recaptcha-wrapper"></div>

          <button type="submit" class="btn-submit" :disabled="isLoading">
            {{ isLoading ? "Sending..." : "Submit" }}
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { Notyf } from 'notyf';
import 'notyf/notyf.min.css';

const notyf = new Notyf();

const isOpen = ref(false);
const isLoading = ref(false);

const name = ref("");
const email = ref("");
const subject = ref("");
const message = ref("");

const SITE_KEY = import.meta.env.VITE_RECAPTCHA_SITE_KEY;
const recaptchaContainer = ref(null);
const recaptchaWidgetId = ref(null);
const recaptchaToken = ref('');

const accessKey = import.meta.env.VITE_WEB3FORMS_ACCESS_KEY;

function onRecaptchaSuccess(token) { recaptchaToken.value = token; }
function onRecaptchaExpired() { recaptchaToken.value = ''; }

function renderRecaptcha() {
  if (window.grecaptcha && recaptchaContainer.value) {
    recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
      sitekey: SITE_KEY,
      size: 'normal',
      callback: onRecaptchaSuccess,
      'expired-callback': onRecaptchaExpired
    });
  }
}

function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null) {
    window.grecaptcha.reset(recaptchaWidgetId.value);
    recaptchaToken.value = '';
  }
}

const handleSubmit = async () => {
  if (!recaptchaToken.value) {
    notyf.error("Please verify that you are not a robot.");
    return;
  }

  isLoading.value = true;
  try {
    const response = await fetch("https://api.web3forms.com/submit", {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'Accept': 'application/json' },
      body: JSON.stringify({
        access_key: accessKey,
        name: name.value,
        email: email.value,
        subject: subject.value,
        message: message.value
      })
    });
    const result = await response.json();
    if (result.success) {
      notyf.success("Message Sent!");
      name.value = email.value = subject.value = message.value = '';
      isOpen.value = false;
      resetRecaptcha();
    } else {
      notyf.error("Failed to send message.");
    }
  } catch (error) {
    console.error(error);
    notyf.error("Failed to send message.");
  } finally {
    isLoading.value = false;
  }
};

onMounted(() => {
  const waitForRecaptcha = () => {
    if (window.grecaptcha && recaptchaContainer.value) renderRecaptcha();
    else requestAnimationFrame(waitForRecaptcha);
  };
  waitForRecaptcha();
});
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
  gap: 0.5rem;
  background-color: #0d6efd;
  color: #fff;
  border: none;
  border-radius: 32px;
  padding: 0.6rem 1.2rem;
  font-weight: 500;
  font-size: 0.9rem;
  cursor: pointer;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.25);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.contact-float-btn:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.3);
}

.btn-icon {
  font-size: 1.1rem;
  animation: wave 2s infinite;
}

@keyframes wave {

  0%,
  60%,
  100% {
    transform: rotate(0deg);
  }

  20% {
    transform: rotate(15deg);
  }

  40% {
    transform: rotate(-15deg);
  }
}

/* Modal */
.contact-modal {
  position: fixed;
  inset: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 998;
}

.overlay-bg {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.55);
  cursor: pointer;
}

/* Contact Container */
.contact-container {
  position: relative;
  width: 100%;
  max-width: 420px;
  background-color: #031624;
  border: 1px solid rgba(13, 110, 253, 0.25);
  border-radius: 12px;
  padding: 2rem;
  color: #fff;
  z-index: 1;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.4);
  transform: translateY(-20px);
  opacity: 0;
  transition: all 0.3s ease;
}

.contact-container.show {
  transform: translateY(0);
  opacity: 1;
}

/* Header */
.contact-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.contact-header h5 {
  font-size: 1.3rem;
  font-weight: 500;
}

.close-btn {
  background: transparent;
  border: none;
  font-size: 1.5rem;
  color: #fff;
  cursor: pointer;
}

/* Inputs */
.contact-container input,
.contact-container textarea {
  width: 100%;
  background-color: #0d1b2a;
  border: 1px solid rgba(13, 110, 253, 0.2);
  color: #fff;
  padding: 0.55rem 0.7rem;
  border-radius: 6px;
  margin-bottom: 0.9rem;
  font-size: 0.85rem;
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
}

.contact-container input:focus,
.contact-container textarea:focus {
  border-color: #0d6efd;
  outline: none;
  box-shadow: 0 0 0 2px rgba(13, 110, 253, 0.2);
}

/* Submit Button */
.btn-submit {
  background-color: #0d6efd;
  color: #fff;
  font-weight: 500;
  padding: 0.6rem;
  border-radius: 8px;
  border: none;
  font-size: 0.9rem;
  width: 100%;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn-submit:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.35);
}

/* reCAPTCHA */
.recaptcha-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}

/* Responsive */
@media (max-width: 768px) {
  .contact-container {
    width: 90%;
    padding: 1.5rem;
  }

  .contact-float-btn {
    padding: 0.45rem 1rem;
    font-size: 0.8rem;
  }

  .btn-icon {
    font-size: 1rem;
  }
}
</style>