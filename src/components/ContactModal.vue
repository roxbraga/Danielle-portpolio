
<script setup lang="ts">
import { ref, watch, onUnmounted } from 'vue'

const props = defineProps<{
  isOpen: boolean
}>()

const emit = defineEmits<{
  (event: 'close'): void
}>()

const isSending = ref(false)
const submissionStatus = ref<'success' | 'error' | ''>('')
const submissionMessage = ref('')

const closeModal = () => {
  emit('close')
}

const handleEscape = (event: KeyboardEvent) => {
  if (event.key === 'Escape' && props.isOpen) {
    closeModal()
  }
}

watch(
  () => props.isOpen,
  (isOpen) => {
    document.body.style.overflow = isOpen ? 'hidden' : ''

    if (isOpen) {
      document.addEventListener('keydown', handleEscape)
    } else {
      document.removeEventListener('keydown', handleEscape)
      submissionStatus.value = ''
      submissionMessage.value = ''
    }
  },
  { immediate: true }
)

onUnmounted(() => {
  document.removeEventListener('keydown', handleEscape)
  document.body.style.overflow = ''
})

const sendMessage = async (event: Event) => {
  const form = event.currentTarget as HTMLFormElement

  if (isSending.value) return

  isSending.value = true
  submissionStatus.value = ''
  submissionMessage.value = ''

  try {
    const formData = new FormData(form)

    formData.append(
      '_subject',
      `Portfolio Inquiry from ${String(formData.get('name') || 'Visitor')}`
    )

    const response = await fetch(
      'https://formspree.io/f/xaeolpya',
      {
        method: 'POST',
        body: formData,
        headers: {
          Accept: 'application/json',
        },
      }
    )

    if (!response.ok) {
      throw new Error('Form submission failed.')
    }

    submissionStatus.value = 'success'
    submissionMessage.value =
      "Message sent successfully! Thank you for reaching out. I'll get back to you soon."

    form.reset()
  } catch (error) {
    console.error('Contact form error:', error)

    submissionStatus.value = 'error'
    submissionMessage.value =
      'Failed to send your message. Please try again in a moment.'
  } finally {
    isSending.value = false
  }
}
</script>

<template>
  <Teleport to="body">
    <div v-if="isOpen" class="contact-modal-overlay">
      <div
        class="contact-modal"
        role="dialog"
        aria-modal="true"
        aria-labelledby="contact-modal-title"
      >
        <button
          type="button"
          class="contact-modal-back"
          @click="closeModal"
        >
          ← Back to Portfolio
        </button>

        <button
          type="button"
          class="contact-modal-close"
          aria-label="Close contact form"
          @click="closeModal"
        >
          ×
        </button>

        <div class="contact-modal-content">
          <!-- LEFT SIDE -->
          <div class="contact-modal-info">
            <span class="contact-modal-eyebrow">GET IN TOUCH</span>

            <h2 id="contact-modal-title">
              Let's Work
              <br />
              Together
            </h2>

            <span class="contact-modal-underline"></span>

            <p class="contact-modal-description">
              Have a project, role, or opportunity in mind?
              I'd love to hear from you. Send me a message
              and I'll get back to you as soon as possible.
            </p>

            <div class="contact-info-list">
              <div class="contact-info-item">
                <div class="contact-info-icon">✉</div>
                <div>
                  <h3>Email</h3>
                  <a href="mailto:daniabulad@gmail.com">
                    daniabulad@gmail.com
                  </a>
                </div>
              </div>

              <div class="contact-info-item">
                <div class="contact-info-icon">📍</div>
                <div>
                  <h3>Location</h3>
                  <span>Quezon, Philippines</span>
                </div>
              </div>

              <div class="contact-info-item">
                <div class="contact-info-icon">📞</div>
                <div>
                  <h3>Mobile Number</h3>
                  <a href="tel:09952828784">09952828784</a>
                </div>
              </div>
            </div>
          </div>

          <!-- RIGHT SIDE FORM -->
          <div class="contact-modal-form-wrapper">
            <form
              class="contact-form"
              @submit.prevent="sendMessage"
            >
              <div class="contact-form-row">
                <div class="contact-form-group">
                  <label for="contact-name">
                    Your Name <span>*</span>
                  </label>

                  <input
                    id="contact-name"
                    type="text"
                    name="name"
                    placeholder="Enter your name"
                    autocomplete="name"
                    required
                    :disabled="isSending"
                  />
                </div>

                <div class="contact-form-group">
                  <label for="contact-email">
                    Your Email <span>*</span>
                  </label>

                  <input
                    id="contact-email"
                    type="email"
                    name="email"
                    placeholder="Enter your email"
                    autocomplete="email"
                    required
                    :disabled="isSending"
                  />
                </div>
              </div>

              <div class="contact-form-group contact-message-group">
                <label for="contact-message">
                  Your Message <span>*</span>
                </label>

                <textarea
                  id="contact-message"
                  name="message"
                  placeholder="Tell me about the project, role, or opportunity..."
                  rows="4"
                  required
                  :disabled="isSending"
                ></textarea>
              </div>

              <!-- SUBMISSION NOTIFICATION -->
              <div
                v-if="submissionStatus"
                class="contact-form-notification"
                :class="`notification-${submissionStatus}`"
                role="status"
                aria-live="polite"
              >
                <span class="notification-icon">
                  {{ submissionStatus === 'success' ? '✓' : '!' }}
                </span>

                <span>{{ submissionMessage }}</span>
              </div>

              <!-- SEND BUTTON AND SOCIAL LINKS -->
              <div class="contact-form-bottom">
                <button
                  type="submit"
                  class="contact-submit-button"
                  :disabled="isSending"
                >
                  <span v-if="isSending" class="contact-loading-spinner"></span>
                  <span v-else>➤</span>

                  {{ isSending ? 'Sending...' : 'Send Message' }}
                </button>

                <div class="contact-social-links">
                  <a
                    class="contact-social-link"
                    href="YOUR_LINKEDIN_URL"
                    target="_blank"
                    rel="noopener noreferrer"
                    aria-label="LinkedIn"
                    title="LinkedIn"
                  >
                    <img
                      src="https://upload.wikimedia.org/wikipedia/commons/c/ca/LinkedIn_logo_initials.png"
                      alt="LinkedIn"
                    />
                  </a>

                  <a
                    class="contact-social-link"
                    href="YOUR_INDEED_URL"
                    target="_blank"
                    rel="noopener noreferrer"
                    aria-label="Indeed"
                    title="Indeed"
                  >
                    <img
                      src="https://svgicons.com/img/188816/indeed.svg"
                      alt="Indeed"
                    />
                  </a>

                  <a
                    class="contact-social-link"
                    href="YOUR_ONLINEJOBS_PROFILE_URL"
                    target="_blank"
                    rel="noopener noreferrer"
                    aria-label="OnlineJobs.ph"
                    title="OnlineJobs.ph"
                  >
                    <img
                      src="/images.png"
                      alt="OnlineJobs.ph"
                    />
                  </a>

                  <a
                    class="contact-social-link"
                    href="mailto:daniabulad@gmail.com"
                    aria-label="Gmail"
                    title="Gmail"
                  >
                    <img
                      src="https://cdn.simpleicons.org/gmail/EA4335"
                      alt="Gmail"
                    />
                  </a>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>
