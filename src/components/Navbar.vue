
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits<{
  (event: 'open-contact'): void
}>()

const navLinks = [
  { label: 'Home', href: '#home' },
  { label: 'About', href: '#about' },
  { label: 'Services', href: '#services' },
  { label: 'Tools', href: '#tools' },
  { label: 'Testimonials', href: '#testimonials' },
  { label: 'Contact', href: '#contact' },
]

const activeSection = ref('home')

let observer: IntersectionObserver | null = null

const closeMobileMenu = () => {
  const navbarCollapse = document.getElementById('portfolioNavbar')

  if (navbarCollapse?.classList.contains('show')) {
    const toggler = document.querySelector<HTMLButtonElement>(
      '.navbar-toggler'
    )

    toggler?.click()
  }
}

const navigateTo = (href: string) => {
  activeSection.value = href.replace('#', '')
  closeMobileMenu()
}

const handleContactClick = () => {
  closeMobileMenu()
  emit('open-contact')
}

onMounted(() => {
  const sections = navLinks
    .filter((link) => link.href !== '#contact')
    .map((link) => document.querySelector(link.href))
    .filter((section): section is Element => section !== null)

  observer = new IntersectionObserver(
    (entries) => {
      const visibleSections = entries
        .filter((entry) => entry.isIntersecting)
        .sort(
          (a, b) =>
            b.intersectionRatio - a.intersectionRatio
        )

      if (visibleSections.length > 0) {
        activeSection.value = visibleSections[0].target.id
      }
    },
    {
      rootMargin: '-20% 0px -60% 0px',
      threshold: [0, 0.1, 0.25, 0.5],
    }
  )

  sections.forEach((section) => observer?.observe(section))
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>

<template>
  <nav class="navbar navbar-expand-lg portfolio-navbar sticky-top">
    <div class="container">

      <a class="navbar-brand d-flex align-items-center gap-2" href="#home">
        <span class="brand-info">
          <span class="brand-name">Danielle Abulad</span>
          <span class="brand-subtitle">
            E-Commerce Virtual Assistant
          </span>
        </span>
      </a>

      <button
        class="navbar-toggler custom-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#portfolioNavbar"
        aria-controls="portfolioNavbar"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="menu-icon">☰</span>
      </button>

      <div class="collapse navbar-collapse" id="portfolioNavbar">
        <ul class="navbar-nav mx-auto align-items-lg-center">
          <li
            v-for="link in navLinks"
            :key="link.label"
            class="nav-item"
          >
            <a
              v-if="link.label !== 'Contact'"
              class="nav-link"
              :class="{
                active: activeSection === link.href.replace('#', '')
              }"
              :href="link.href"
              @click="navigateTo(link.href)"
            >
              {{ link.label }}
            </a>

            <button
              v-else
              type="button"
              class="nav-link"
              @click="handleContactClick"
            >
              {{ link.label }}
            </button>
          </li>
        </ul>

        <a
          class="btn get-in-touch-btn"
          href="/Danielle%20VA.pdf"
          download="Danielle VA.pdf"
        >
          Download CV
          <span class="mail-icon">↓</span>
        </a>
      </div>

    </div>
  </nav>
</template>
