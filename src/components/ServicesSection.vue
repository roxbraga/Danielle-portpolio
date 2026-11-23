
<script setup lang="ts">
const services = [
  {
    title: 'Order & Fulfilment Management',
    description:
      'Monitor orders, follow up on fulfilment, and resolve order issues.',
    icon: 'cart',
  },
  {
    title: 'Invoicing & Administration',
    description:
      'Process and track invoices, manage POs, and ensure accurate records.',
    icon: 'invoice',
  },
  {
    title: 'Retailer Success & Outreach',
    description:
      'Onboard, assist, and maintain strong relationships with retail partners.',
    icon: 'people',
  },
  {
    title: 'Customer & Brand Coordination',
    description:
      'Handle retailer inquiries, follow-ups, and account updates.',
    icon: 'support',
  },
  {
    title: 'Operations & Workflow Support',
    description:
      'Keep tasks organized, create trackers, and improve team processes.',
    icon: 'settings',
  },
]
</script>

<template>
  <section id="services" class="services-section">
    <div class="container">
      <div class="services-heading">
        <span class="section-eyebrow">SERVICES</span>
        <h2>How I Can Support Your Business</h2>
      </div>

      <div class="services-grid">
        <article
          v-for="service in services"
          :key="service.title"
          class="service-card"
        >
          <div class="service-icon">
            <svg
              v-if="service.icon === 'cart'"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <circle cx="9" cy="20" r="1" />
              <circle cx="19" cy="20" r="1" />
              <path d="M1 2h3l2.5 12.5a2 2 0 0 0 2 1.5h9.8a2 2 0 0 0 2-1.6L22 7H5" />
            </svg>

            <svg
              v-else-if="service.icon === 'invoice'"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M6 2h9l5 5v15H6z" />
              <path d="M15 2v6h5M9 12h8M9 16h8" />
            </svg>

            <svg
              v-else-if="service.icon === 'people'"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <circle cx="9" cy="8" r="3" />
              <path d="M3 20v-2a6 6 0 0 1 12 0v2z" />
              <circle cx="18" cy="9" r="2.5" />
              <path d="M17 15a5 5 0 0 1 4 5" />
            </svg>

            <svg
              v-else-if="service.icon === 'support'"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M3 13v-2a9 9 0 0 1 18 0v2" />
              <rect x="2" y="12" width="4" height="7" rx="2" />
              <rect x="18" y="12" width="4" height="7" rx="2" />
              <path d="M18 19a6 6 0 0 1-6 3h-1" />
            </svg>

            <svg
              v-else
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <circle cx="12" cy="12" r="3" />
              <path d="M19.4 15a1.7 1.7 0 0 0 .3 1.9l.1.1-1.7 2.9-.2-.1a1.7 1.7 0 0 0-1.8.1l-.2.1h-3.4l-.1-.2a1.7 1.7 0 0 0-1.6-1h-.2l-2.9-1.7.1-.2a1.7 1.7 0 0 0-.1-1.8l-.1-.2v-3.4l.2-.1a1.7 1.7 0 0 0 1-1.6v-.2l1.7-2.9.2.1a1.7 1.7 0 0 0 1.8-.1l.2-.1h3.4l.1.2a1.7 1.7 0 0 0 1.6 1h.2l2.9 1.7-.1.2a1.7 1.7 0 0 0 .1 1.8l.1.2v3.4z" />
            </svg>
          </div>

          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
        </article>
      </div>
    </div>
  </section>
</template>
