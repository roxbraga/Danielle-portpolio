
<script setup lang="ts">
const tools = [
  'Intercom',
  'HubSpot',
  'Zendesk',
  'Slack',
  'B2B E-commerce Marketplace',
  'Shopify',
  'HEX',
  'Structify',
  'Google Workspace',
  'Microsoft Office',
  'Excel',
  'Notion',
  'Canva',
  'Adobe Premiere Pro',
  'CapCut',
  'AI Tools - Proper Prompting',
  'Claude',
  'ChatGPT',
  'Gemini',
]

const duplicatedTools = [...tools, ...tools]
</script>

<template>
  <section id="tools" class="tools-section">
    <div class="container">
      <div class="tools-layout">

        <!-- Fixed Heading -->
        <div class="tools-heading">
          <span class="section-eyebrow">TOOLS & PLATFORMS</span>
          <h2>Systems I Work With Daily</h2>
        </div>

        <!-- Moving Carousel -->
        <div class="tools-carousel">
          <div class="tools-track">
            <div
              v-for="(tool, index) in duplicatedTools"
              :key="`${tool}-${index}`"
              class="tools-group"
            >
              <span class="tool-pill">
                <span class="tool-dot"></span>
                {{ tool }}
              </span>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
