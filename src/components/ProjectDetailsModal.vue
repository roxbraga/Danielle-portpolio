
<script setup lang="ts">
import {
  computed,
  onBeforeUnmount,
  onMounted,
  ref,
  watch,
} from 'vue'

import type { WorkProject } from '../types/workProject'

const props = defineProps<{
  project: WorkProject | null
}>()

const emit = defineEmits<{
  close: []
}>()

const activeImageIndex = ref(0)

const activeImage = computed(() => {
  return props.project?.images[activeImageIndex.value] ?? ''
})

const nextImage = () => {
  if (!props.project) return

  activeImageIndex.value =
    (activeImageIndex.value + 1) % props.project.images.length
}

const previousImage = () => {
  if (!props.project) return

  activeImageIndex.value =
    (activeImageIndex.value - 1 + props.project.images.length) %
    props.project.images.length
}

const selectImage = (index: number) => {
  activeImageIndex.value = index
}

const handleKeyboard = (event: KeyboardEvent) => {
  if (!props.project) return

  if (event.key === 'Escape') emit('close')
  if (event.key === 'ArrowRight') nextImage()
  if (event.key === 'ArrowLeft') previousImage()
}

watch(
  () => props.project,
  (project) => {
    activeImageIndex.value = 0

    if (typeof document !== 'undefined') {
      document.body.style.overflow = project ? 'hidden' : ''
    }
  },
  { immediate: true },
)

onMounted(() => {
  window.addEventListener('keydown', handleKeyboard)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeyboard)
  document.body.style.overflow = ''
})
</script>

<template>
  <Transition name="project-modal">
    <div
      v-if="project"
      class="project-modal-overlay"
      @click.self="emit('close')"
    >
      <div
        class="project-modal-container"
        role="dialog"
        aria-modal="true"
        :aria-label="project.title"
      >

        <!-- CLOSE BUTTON -->
        <button
          type="button"
          class="project-modal-close"
          aria-label="Close project details"
          @click="emit('close')"
        >
          &times;
        </button>

        <div class="project-modal-body">

          <!-- LEFT SIDE: PROJECT DETAILS -->
          <div class="project-modal-details">

            <span class="project-modal-label">
              <span class="project-label-dot"></span>
              WORK HIGHLIGHT
            </span>

            <h2>{{ project.title }}</h2>

            <span class="project-modal-category">
              {{ project.category }}
            </span>

            <p class="project-modal-overview">
              {{ project.overview }}
            </p>

            <div class="project-modal-divider"></div>

            <h3>What It Covers</h3>

            <ul class="project-feature-list">
              <li
                v-for="feature in project.features"
                :key="feature"
              >
                <span class="project-check-icon">✓</span>
                <span>{{ feature }}</span>
              </li>
            </ul>

            <!-- TOOLS -->
            <div class="project-modal-tools-section">
              <h3>Tools Used</h3>

              <div class="project-modal-tools">
                <span
                  v-for="tool in project.tools"
                  :key="tool"
                  class="project-modal-tool"
                >
                  {{ tool }}
                </span>
              </div>

              <!-- SKILLS -->
              <h3 class="project-modal-skills-heading">
                Skills Demonstrated
              </h3>

              <div class="project-modal-tools">
                <span
                  v-for="skill in project.skills"
                  :key="skill"
                  class="project-modal-skill"
                >
                  {{ skill }}
                </span>
              </div>
            </div>

          </div>

          <!-- RIGHT SIDE: IMAGE GALLERY -->
          <div class="project-modal-gallery">

            <div class="project-main-image">
              <img
                :src="activeImage"
                :alt="`${project.title} screenshot ${activeImageIndex + 1}`"
              />

              <span class="project-image-counter">
                {{ activeImageIndex + 1 }}
                /
                {{ project.images.length }}
              </span>
            </div>

            <!-- GALLERY NAVIGATION -->
            <div class="project-gallery-controls">

              <button
                type="button"
                class="project-gallery-arrow"
                aria-label="Previous screenshot"
                @click="previousImage"
              >
                ‹
              </button>

              <div class="project-thumbnails">

                <button
                  v-for="(image, index) in project.images"
                  :key="image"
                  type="button"
                  class="project-thumbnail"
                  :class="{
                    active: activeImageIndex === index,
                  }"
                  :aria-label="`Show screenshot ${index + 1}`"
                  :aria-pressed="activeImageIndex === index"
                  @click="selectImage(index)"
                >
                  <img
                    :src="image"
                    :alt="`Preview ${index + 1}`"
                  />
                </button>

              </div>

              <button
                type="button"
                class="project-gallery-arrow"
                aria-label="Next screenshot"
                @click="nextImage"
              >
                ›
              </button>

            </div>

            <p class="project-gallery-caption">
              Project Preview · {{ project.title }}
            </p>

          </div>

        </div>

        <!-- FOOTER -->
        <div class="project-modal-footer">

          <span class="project-modal-footer-note">
            Selected Work · Danielle Abulad
          </span>

          <button
            type="button"
            class="project-modal-done-btn"
            @click="emit('close')"
          >
            Close
            <span aria-hidden="true">→</span>
          </button>

        </div>

      </div>
    </div>
  </Transition>
</template>
