
<script setup lang="ts">
import { computed, ref } from 'vue'

const activeIndex = ref(0)

const testimonials = [
  {
    name: 'Elian Haddock',
    role: 'COO, Airgoods',
    image: '/elian.jpg',
    message:
      "Wanted to give a quick shoutout to Danielle! She's been notifying some of our retailers about the spring discount week and had the great idea to create multiple email templates with different subject lines and email body, and send in batches spaced out so it's less likely to end up in Spam folder.",
  },
  {
    name: 'Trix Montemayor',
    role: 'Team Leader, Airgoods',
    image: '/trix-profile.png',
    message:
      "This month, I'd like to nominate Danielle. She's definitely one of Airgoods' assets, and the trust Elian has in her to handle tasks on his behalf says a lot about her. She's also very dependable, never missing work and always willing to step in whenever Loyce or I need backup. Her love for what she does is evident in her work ethic, and that's something truly worth recognizing!",
  },
  {
    name: 'Loyce Salumbides',
    role: 'Colleague, Airgoods',
    image: '/loyce-profile.png',
    message:
      "Danielle has always been someone I could count on. She's proactive, easy to work with, and always willing to help whenever the team needs extra support. She takes ownership of her responsibilities, pays attention to details, and makes sure things are handled properly. It was a pleasure working alongside her at Airgoods!",
  },
]

const displayedTestimonials = computed(() => [
  ...testimonials.slice(activeIndex.value),
  ...testimonials.slice(0, activeIndex.value),
])

const nextSlide = () => {
  activeIndex.value = (activeIndex.value + 1) % testimonials.length
}

const previousSlide = () => {
  activeIndex.value =
    (activeIndex.value - 1 + testimonials.length) % testimonials.length
}
</script>

<template>
  <section id="testimonials" class="testimonials-section">
    <div class="container">
      <div class="testimonials-layout">

        <!-- Section Heading -->
        <div class="testimonials-heading">
          <span class="section-eyebrow">TESTIMONIALS</span>

          <h2>
            What People Say
            <br />
            About My Work
          </h2>

          <span class="testimonial-underline"></span>
        </div>

        <!-- Testimonial Carousel -->
        <div class="testimonial-carousel">

          <button
            type="button"
            class="testimonial-arrow testimonial-arrow-left"
            aria-label="Previous testimonials"
            @click="previousSlide"
          >
            ‹
          </button>

          <div class="testimonial-cards">
            <article
              v-for="testimonial in displayedTestimonials"
              :key="testimonial.name"
              class="testimonial-card"
            >
              <span class="testimonial-quote">“</span>

              <p class="testimonial-message">
                {{ testimonial.message }}
              </p>

              <div class="testimonial-author">
                <img
                  :src="testimonial.image"
                  :alt="testimonial.name"
                  class="testimonial-avatar"
                />

                <div class="testimonial-author-info">
                  <h3>{{ testimonial.name }}</h3>
                  <span>{{ testimonial.role }}</span>
                </div>
              </div>
            </article>
          </div>

          <button
            type="button"
            class="testimonial-arrow testimonial-arrow-right"
            aria-label="Next testimonials"
            @click="nextSlide"
          >
            ›
          </button>

        </div>
      </div>

      <!-- Pagination -->
      <div class="testimonial-dots">
        <button
          v-for="(_, index) in testimonials"
          :key="index"
          type="button"
          :class="{ active: activeIndex === index }"
          :aria-label="`Show testimonial set ${index + 1}`"
          @click="activeIndex = index"
        ></button>
      </div>

    </div>
  </section>
</template>
