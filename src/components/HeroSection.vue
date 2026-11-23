
<script setup lang="ts">
import { ref } from 'vue'

const videoSource = '/vid1.mp4'
const videoRef = ref<HTMLVideoElement | null>(null)

const playIntroduction = async () => {
  const video = videoRef.value

  if (!video) {
    console.error('Introduction video element not found.')
    return
  }

  try {
    video.muted = false

    await video.play()

    video.scrollIntoView({
      behavior: 'smooth',
      block: 'center',
    })
  } catch (error) {
    console.error('Unable to play introduction video:', error)
  }
}
</script>

<template>
  <section id="home" class="hero-section">
    <div class="container">
      <div class="row align-items-center g-4">

        <!-- Hero Content -->
        <div class="col-lg-5">
          <div class="hero-content">

            <span class="hero-eyebrow">
              E-COMMERCE VIRTUAL ASSISTANT
            </span>

            <h1 class="hero-title">
              Streamlining E-Commerce Operations and Supporting
              <span>Business Growth</span>
            </h1>

            <p class="hero-description">
              I help e-commerce and retail brands stay organized,
              keep orders moving, manage operations, and support
              retailer success so you can focus on growing your business.
            </p>

            <div class="hero-actions">
              <button
                type="button"
                class="hero-btn hero-btn-primary"
                @click="playIntroduction"
              >
                <span class="play-icon">▶</span>
                Watch My Introduction
              </button>

              <a
                href="#services"
                class="hero-btn hero-btn-outline"
              >
                View My Services
                <span>→</span>
              </a>
            </div>

          </div>
        </div>

        <!-- Introduction Video -->
        <div class="col-lg-7">
          <div
            id="introduction-video"
            class="hero-video-wrapper"
          >
            <video
              ref="videoRef"
              class="hero-video"
              controls
              playsinline
              preload="metadata"
              poster="/danielle-thumbnail.jpg"
            >
              <source
                :src="videoSource"
                type="video/mp4"
              />

              Your browser does not support HTML video.
            </video>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
