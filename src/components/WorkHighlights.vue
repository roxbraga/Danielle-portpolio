
<script setup lang="ts">
import { ref } from 'vue'
import ProjectDetailsModal from './ProjectDetailsModal.vue'
import type { WorkProject } from '../types/workProject'

const selectedProject = ref<WorkProject | null>(null)

const projects: WorkProject[] = [
  {
    id: 1,
    title: 'Retailer Onboarding & Automated Tracking System',
    category: 'Retailer Success & Workflow Automation',
    description:
      'Created and maintained a Notion-based tracking system for large retailer onboarding and Free Fill requests. Connected email and Quo (US SMS) communication workflows to help automatically update tracking records when responses are received, making it easier to monitor brand confirmations, communication history, and pending follow-up actions.',
    overview:
      'Created and maintained a Notion-based tracking system for large retailer onboarding and Free Fill requests. Connected email and Quo (US SMS) communication workflows to help automatically update tracking records when responses are received, making it easier to monitor brand confirmations, communication history, and pending follow-up actions.',
    coverImage: '/order-tracker-1.jpg',
    images: [
      '/order-tracker-1.jpg'
    ],
    tools: ['Notion', 'Email', 'Quo'],
    skills: [
      'Workflow Automation',
      'Retailer Coordination',
      'Communication Management',
      'Data Tracking',
    ],
    features: [
      'Retailer onboarding tracking',
      'Free Fill request monitoring',
      'Email and SMS communication workflows',
      'Brand confirmation tracking',
      'Communication history management',
      'Pending follow-up monitoring',
    ],
  },
  {
    id: 2,
    title: 'Purchase Order Processing & Invoice Management',
    category: 'B2B Operations & Administration',
    description:
      'Handled retailer purchase order coordination through ECRS Gateway and managed invoice submission and tracking for B2B retail accounts. Received purchase order notifications, reviewed attached documents, sent invoices to Accounts Payable contacts, and maintained an invoice tracker to monitor submission status and due dates.',
    overview:
      'Handled retailer purchase order coordination through ECRS Gateway and managed invoice submission and tracking for B2B retail accounts. Received purchase order notifications, reviewed attached documents, sent invoices to Accounts Payable contacts, and maintained an invoice tracker to monitor submission status and due dates.',
    coverImage: '/invoicing-1.jpg',
    images: [
      '/invoicing-1.jpg',
      '/invoicing-2.jpg',
      '/invoicing-3.jpg',
    ],
    tools: ['ECRS Gateway', 'Email', 'P2 Admin', 'Notion'],
    skills: [
      'Purchase Order Processing',
      'Invoice Submission',
      'Invoice Tracking',
      'Accounts Payable Coordination',
      'Administrative Support',
    ],
    features: [
      'Purchase order notification monitoring',
      'Purchase order document review',
      'Invoice submission to Accounts Payable contacts',
      'Invoice status tracking',
      'Invoice due date monitoring',
      'B2B retail account coordination',
    ],
  },
  {
    id: 3,
    title: 'Customer Support – Airgoods Website & Shopify Integration Assistance',
    category: 'Customer Support & E-Commerce',
    description:
      "Provided customer support through the Airgoods website, assisting brands with platform-related concerns, including shipping inquiries and Shopify integration issues. Explained shipping payment options and shipping label processes. For integration-related concerns, investigated product import and inventory errors, reset product linking between Airgoods and Shopify, and accepted affected orders on the customer's behalf.",
    overview:
      "Provided customer support through the Airgoods website, assisting brands with platform-related concerns, including shipping inquiries and Shopify integration issues. Explained shipping payment options and shipping label processes. For integration-related concerns, investigated product import and inventory errors, reset product linking between Airgoods and Shopify, and accepted affected orders on the customer's behalf.",
    coverImage: '/retailer-report-1.jpg',
    images: [
      '/retailer-report-1.jpg',
      '/retailer-report-2.jpg',
    ],
    tools: ['Airgoods Website', 'Shopify', 'Intercom'],
    skills: [
      'Customer Support',
      'E-commerce Platform Support',
      'Shopify Integration Assistance',
      'Order Management',
      'Problem-Solving',
    ],
    features: [
      'Brand support through the Airgoods website',
      'Shipping inquiries and payment options',
      'Shipping label process assistance',
      'Shopify product import troubleshooting',
      'Inventory synchronization issue investigation',
      'Product linking reset between platforms',
      'Order acceptance assistance',
    ],
  },
]

const openProject = (project: WorkProject) => {
  selectedProject.value = project
}

const closeProject = () => {
  selectedProject.value = null
}
</script>

<template>
  <section id="work-highlights" class="work-highlights">
    <div class="container">

      <!-- SECTION HEADER -->
      <div class="work-section-heading">
        <span class="work-section-label">
          WORK HIGHLIGHTS
        </span>

        <h2>What I've Worked On</h2>

        <p>
          A closer look at the projects and workflows I help manage.
        </p>
      </div>

      <!-- PROJECT CARDS -->
      <div class="row g-4">
        <div
          v-for="project in projects"
          :key="project.id"
          class="col-12 col-md-6 col-lg-4"
        >
          <article class="work-card">

            <!-- CARD IMAGE -->
            <div class="work-card-image">
              <img
                :src="project.coverImage"
                :alt="project.title"
                loading="lazy"
              />

              <!-- <span class="work-project-number">
                0{{ project.id }}
              </span> -->
            </div>

            <!-- CARD CONTENT -->
            <div class="work-card-content">

              <span class="work-project-category">
                {{ project.category }}
              </span>

              <h3 class="work-card-title">
                {{ project.title }}
              </h3>

              <p class="work-card-description">
                {{ project.description }}
              </p>

              <!-- VIEW DETAILS BUTTON -->
              <button
                type="button"
                class="work-view-details-btn"
                @click="openProject(project)"
              >
                View Details
                <span aria-hidden="true">→</span>
              </button>

            </div>
          </article>
        </div>
      </div>
    </div>

    <!-- DETAILS MODAL -->
    <ProjectDetailsModal
      :project="selectedProject"
      @close="closeProject"
    />
  </section>
</template>
