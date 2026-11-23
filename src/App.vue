<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import ToolsSection from './components/ToolsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import FooterSection from './components/FooterSection.vue'
import ContactModal from './components/ContactModal.vue'

const isContactOpen = ref(false)

const openContact = () => {
  if (isContactOpen.value) return

  isContactOpen.value = true

  window.history.pushState(
    { contactModal: true },
    '',
    window.location.pathname + window.location.search + '#contact'
  )
}

const closeContact = () => {
  if (!isContactOpen.value) return

  if (window.history.state?.contactModal) {
    window.history.back()
  } else {
    isContactOpen.value = false
  }
}

const handlePopState = () => {
  isContactOpen.value = false
}

onMounted(() => {
  window.addEventListener('popstate', handlePopState)
})

onUnmounted(() => {
  window.removeEventListener('popstate', handlePopState)
})
</script>

<template>
  <div class="portfolio-wrapper">
    <Navbar @open-contact="openContact" />

    <main>
      <HeroSection />
      <AboutSection />
      <ServicesSection />
      <ToolsSection />
      <TestimonialsSection />
    </main>

    <FooterSection @open-contact="openContact" />

    <ContactModal
      :is-open="isContactOpen"
      @close="closeContact"
    />
  </div>
</template>
