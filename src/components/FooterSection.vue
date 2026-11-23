
<script setup lang="ts">
const emit = defineEmits<{
  (event: 'open-contact'): void
}>()
</script>

<template>
  <section class="contact-cta-section">
    <div class="container">
      <div class="contact-cta">
        <div class="contact-cta-icon">
          <span>✉</span>
        </div>

        <h2>Let's Work Together</h2>

        <p>
          Need a reliable E-Commerce VA to support your
          operations, retailers, or growth initiatives?
        </p>

        <button
          type="button"
          class="contact-cta-button"
          @click="emit('open-contact')"
        >
          Get in Touch
          <span>→</span>
        </button>
      </div>
    </div>
  </section>
</template>
