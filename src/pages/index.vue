<template>
  <q-layout view="lHh Lpr lFf" class="bg-dark text-white">
    <q-header elevated class="bg-dark border-bottom-red q-py-sm">
      <q-toolbar class="container-toolbar justify-between">
        <div class="row items-center q-gutter-sm pointer" @click="goToHome">
          <q-avatar
            size="40px"
            font-size="24px"
            color="primary"
            text-color="white"
            icon="hub"
            class="shadow-red"
          />
          <span class="text-h6 text-weight-bolder tracking-wide text-white">
            Apex<span class="text-primary">CRM</span>
          </span>
        </div>

        <!-- Desktop Navigation Menu -->
        <div class="gt-xs row items-center q-gutter-md">
          <q-btn
            flat
            class="nav-link text-capitalize text-weight-medium"
            label="Features"
            @click="scrollTo('features')"
          />
          <q-btn
            flat
            class="nav-link text-capitalize text-weight-medium"
            label="Interactive Demo"
            @click="scrollTo('demo')"
          />
          <q-btn
            flat
            class="nav-link text-capitalize text-weight-medium"
            label="ROI Calculator"
            @click="scrollTo('roi')"
          />
          <q-btn
            flat
            class="nav-link text-capitalize text-weight-medium"
            label="Reviews"
            @click="scrollTo('testimonials')"
          />
          <q-btn
            flat
            class="nav-link text-capitalize text-weight-medium"
            label="Contact"
            @click="scrollTo('contact')"
          />
        </div>

        <div class="row items-center q-gutter-sm">
          <q-btn
            unelevated
            color="primary"
            label="Get Started"
            class="gt-xs btn-premium text-weight-bold"
            style="border-radius: 8px"
          />
          <q-btn
            flat
            dense
            round
            icon="menu"
            aria-label="Menu"
            class="lt-sm text-white"
            @click="toggleLeftDrawer"
          />
        </div>
      </q-toolbar>
    </q-header>

    <!-- Mobile Navigation Drawer -->
    <q-drawer
      v-model="leftDrawerOpen"
      side="left"
      overlay
      behavior="mobile"
      class="bg-dark text-white border-right-red"
    >
      <div class="q-pa-md row justify-between items-center border-bottom-red">
        <div class="row items-center q-gutter-sm">
          <q-avatar size="32px" color="primary" text-color="white" icon="hub" />
          <span class="text-weight-bolder text-white"
            >Apex<span class="text-primary">CRM</span></span
          >
        </div>
        <q-btn flat round dense icon="close" @click="toggleLeftDrawer" />
      </div>

      <q-list class="q-py-md">
        <q-item clickable v-ripple @click="navigateMobile('features')">
          <q-item-section avatar><q-icon name="star" color="primary" /></q-item-section>
          <q-item-section class="text-weight-bold">Features</q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateMobile('demo')">
          <q-item-section avatar><q-icon name="dashboard" color="primary" /></q-item-section>
          <q-item-section class="text-weight-bold">Interactive Demo</q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateMobile('roi')">
          <q-item-section avatar><q-icon name="calculate" color="primary" /></q-item-section>
          <q-item-section class="text-weight-bold">ROI Calculator</q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateMobile('testimonials')">
          <q-item-section avatar><q-icon name="rate_review" color="primary" /></q-item-section>
          <q-item-section class="text-weight-bold">Reviews</q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateMobile('contact')">
          <q-item-section avatar><q-icon name="mail" color="primary" /></q-item-section>
          <q-item-section class="text-weight-bold">Contact</q-item-section>
        </q-item>

        <q-separator dark class="q-my-md" />

        <div class="q-px-md">
          <q-btn
            unelevated
            color="primary"
            label="Get Started Free"
            class="full-width btn-premium text-weight-bold"
          />
        </div>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <!-- Global Footer -->
    <footer class="bg-dark border-top-red q-py-xl">
      <div class="container q-px-md">
        <div class="row q-col-gutter-lg justify-between">
          <div class="col-12 col-md-4">
            <div class="row items-center q-gutter-sm q-mb-md">
              <q-avatar size="36px" color="primary" text-color="white" icon="hub" />
              <span class="text-h6 text-weight-bolder text-white"
                >Apex<span class="text-primary">CRM</span></span
              >
            </div>
            <p class="text-grey-5 text-subtitle2 text-weight-light" style="max-width: 320px">
              The next-generation Customer Relationship Management platform. Designed for modern
              teams to streamline contacts, close deals, and automate workflows.
            </p>
            <div class="row q-gutter-md q-mt-md">
              <q-btn round flat dense color="grey-5" icon="facebook" href="#" target="_blank" />
              <q-btn
                round
                flat
                dense
                color="grey-5"
                icon="sports_basketball"
                href="#"
                target="_blank"
              />
              <q-btn round flat dense color="grey-5" icon="chat" href="#" target="_blank" />
              <q-btn
                round
                flat
                dense
                color="grey-5"
                icon="alternate_email"
                href="#"
                target="_blank"
              />
            </div>
          </div>

          <div class="col-6 col-sm-4 col-md-2">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">Product</div>
            <ul class="footer-links">
              <li><a href="#" @click.prevent="scrollTo('features')">Features</a></li>
              <li><a href="#" @click.prevent="scrollTo('demo')">Interactive Demo</a></li>
              <li><a href="#" @click.prevent="scrollTo('roi')">ROI Calculator</a></li>
              <li><a href="#">Pricing Plan</a></li>
            </ul>
          </div>

          <div class="col-6 col-sm-4 col-md-2">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">Resources</div>
            <ul class="footer-links">
              <li><a href="#">Documentation</a></li>
              <li><a href="#">API Status</a></li>
              <li><a href="#">Security Policy</a></li>
              <li><a href="#">Support Hub</a></li>
            </ul>
          </div>

          <div class="col-12 col-sm-4 col-md-3">
            <div class="text-subtitle1 text-weight-bold text-white q-mb-md">Stay Connected</div>
            <p class="text-grey-5 text-subtitle2 text-weight-light q-mb-md">
              Subscribe to get latest product updates and sales insights.
            </p>
            <q-input
              dark
              dense
              outlined
              v-model="subscribeEmail"
              placeholder="Your Email Address"
              color="primary"
            >
              <template v-slot:append>
                <q-btn round dense flat icon="send" color="primary" @click="subscribe" />
              </template>
            </q-input>
          </div>
        </div>

        <q-separator dark class="q-my-lg bg-grey-9" />

        <div class="row justify-between items-center text-grey-6 text-caption text-weight-light">
          <div>© {{ new Date().getFullYear() }} ApexCRM Inc. All rights reserved.</div>
          <div class="row q-gutter-md">
            <a href="#" class="footer-bottom-link">Privacy Policy</a>
            <a href="#" class="footer-bottom-link">Terms of Service</a>
            <a href="#" class="footer-bottom-link">Cookie Settings</a>
          </div>
        </div>
      </div>
    </footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const leftDrawerOpen = ref(false)
const subscribeEmail = ref('')

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function goToHome() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}

function navigateMobile(id) {
  leftDrawerOpen.value = false
  setTimeout(() => {
    scrollTo(id)
  }, 300)
}

function subscribe() {
  if (!subscribeEmail.value) {
    $q.notify({
      message: 'Please enter a valid email.',
      color: 'negative',
      icon: 'warning',
      position: 'top-right',
    })
    return
  }
  $q.notify({
    message: 'Thank you for subscribing!',
    color: 'positive',
    icon: 'check',
    position: 'top-right',
  })
  subscribeEmail.value = ''
}
</script>

<style lang="scss">
.container-toolbar {
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.border-bottom-red {
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.border-right-red {
  border-right: 1px solid rgba(217, 4, 41, 0.2);
}

.border-top-red {
  border-top: 1px solid rgba(255, 255, 255, 0.08);
}

.nav-link {
  color: #a1a1aa !important;
  font-size: 0.95rem;
  transition: color 0.3s ease;
  &:hover {
    color: #ffffff !important;
  }
}

.shadow-red {
  box-shadow: 0 0 15px rgba(217, 4, 41, 0.4);
}

.pointer {
  cursor: pointer;
}

.tracking-wide {
  letter-spacing: 0.05em;
}

.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
  li {
    margin-bottom: 8px;
    a {
      color: #a1a1aa;
      text-decoration: none;
      font-size: 0.9rem;
      transition: color 0.2s ease;
      &:hover {
        color: #d90429;
      }
    }
  }
}

.footer-bottom-link {
  color: #71717a;
  text-decoration: none;
  font-size: 0.8rem;
  transition: color 0.2s ease;
  &:hover {
    color: #a1a1aa;
  }
}
</style>
