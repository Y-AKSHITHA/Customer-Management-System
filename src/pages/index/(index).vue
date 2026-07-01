<template>
  <q-page class="q-pb-xl">
    <!-- Hero Section -->
    <section class="hero-section text-center relative-position overflow-hidden q-py-xl">
      <!-- Glow effect behind hero text -->
      <div
        class="absolute-center bg-glow"
        style="
          width: 600px;
          height: 600px;
          opacity: 0.15;
          filter: blur(120px);
          pointer-events: none;
        "
      ></div>

      <div class="container q-px-md column items-center">
        <!-- Badge -->
        <div class="hero-badge q-px-md q-py-xs q-mb-lg row items-center q-gutter-xs">
          <q-icon name="bolt" color="primary" />
          <span class="text-caption text-weight-bold text-uppercase tracking-wider"
            >Version 3.0 is Live</span
          >
        </div>

        <!-- Big Headline -->
        <h1
          class="text-h2 text-weight-bolder q-mt-none q-mb-md text-gradient-red leading-tight"
          style="max-width: 850px"
        >
          Manage Customers. <br class="lt-sm" />
          <span class="text-gradient-full-red">Accelerate Sales.</span> <br />
          Elevate Your Business.
        </h1>

        <!-- Subtitle -->
        <p class="text-subtitle1 text-grey-5 text-weight-light q-mb-xl" style="max-width: 600px">
          The next-generation Customer Relationship Management system designed to simplify contact
          management, automate communication workflows, and drive deal growth.
        </p>

        <!-- CTA Buttons -->
        <div class="row q-gutter-md justify-center q-mb-xl">
          <q-btn
            unelevated
            color="primary"
            label="Get Started Free"
            size="lg"
            class="btn-premium text-weight-bold shadow-red"
            style="border-radius: 8px"
          />
          <q-btn
            outline
            color="white"
            label="Book a Demo"
            size="lg"
            class="text-weight-bold"
            style="border-radius: 8px"
            @click="scrollTo('contact')"
          />
        </div>

        <!-- Interactive Sales Dashboard Preview (Hero Mockup) -->
        <div class="full-width q-px-xs q-px-sm-md" style="max-width: 950px">
          <div
            class="glass-card q-pa-md q-pa-sm-lg relative-position border-gradient shadow-red overflow-hidden"
          >
            <!-- Header bar of dashboard -->
            <div class="row justify-between items-center q-mb-lg">
              <div class="row items-center q-gutter-sm">
                <span class="dot bg-red"></span>
                <span class="dot bg-grey-8"></span>
                <span class="dot bg-grey-8"></span>
                <span class="text-caption text-grey-5 q-ml-sm font-mono"
                  >Live Dashboard Preview</span
                >
              </div>
              <div class="row q-gutter-xs">
                <q-badge
                  color="primary"
                  text-color="white"
                  label="Production Mode"
                  class="q-px-sm q-py-xs"
                />
              </div>
            </div>

            <!-- Dashboard Stats Grid -->
            <div class="row q-col-gutter-md q-mb-lg">
              <div class="col-6 col-sm-3" v-for="stat in previewStats" :key="stat.title">
                <div class="bg-dark-card q-pa-md rounded-borders border-light">
                  <div class="text-caption text-grey-5 text-weight-medium">{{ stat.title }}</div>
                  <div class="text-h6 text-weight-bold text-white q-my-xs">{{ stat.value }}</div>
                  <div
                    class="text-caption text-weight-bold"
                    :class="stat.trendUp ? 'text-positive' : 'text-negative'"
                  >
                    <q-icon :name="stat.trendUp ? 'trending_up' : 'trending_down'" />
                    {{ stat.change }}
                  </div>
                </div>
              </div>
            </div>

            <!-- Pipeline Overview & Sales Activity -->
            <div class="row q-col-gutter-md">
              <div class="col-12 col-md-7">
                <div
                  class="bg-dark-card q-pa-md rounded-borders border-light full-height column justify-between"
                >
                  <div class="row justify-between items-center q-mb-md">
                    <span class="text-weight-bold text-subtitle2 text-white"
                      >Pipeline Distribution</span
                    >
                    <span class="text-caption text-grey-5">Total Value: $485,200</span>
                  </div>
                  <!-- Pipeline Stages with Progress Bars -->
                  <div class="q-gutter-sm">
                    <div v-for="stage in pipelineStats" :key="stage.name">
                      <div class="row justify-between text-caption text-grey-4 q-mb-xs">
                        <span>{{ stage.name }}</span>
                        <span class="text-weight-bold"
                          >{{ stage.value }} ({{ stage.percent }}%)</span
                        >
                      </div>
                      <div class="progress-bar-container bg-grey-9">
                        <div
                          class="progress-bar bg-primary"
                          :style="{ width: stage.percent + '%' }"
                        ></div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="col-12 col-md-5">
                <div class="bg-dark-card q-pa-md rounded-borders border-light full-height">
                  <div class="text-weight-bold text-subtitle2 text-white q-mb-md">
                    Recent CRM Activities
                  </div>
                  <q-list dense>
                    <q-item v-for="act in recentActivities" :key="act.id" class="q-px-none q-py-sm">
                      <q-item-section avatar class="min-width-auto q-pr-sm">
                        <q-avatar
                          size="28px"
                          :color="act.color"
                          text-color="white"
                          :icon="act.icon"
                        />
                      </q-item-section>
                      <q-item-section>
                        <q-item-label class="text-caption text-weight-bold text-white">{{
                          act.user
                        }}</q-item-label>
                        <q-item-label caption class="text-grey-5" style="font-size: 0.75rem">{{
                          act.details
                        }}</q-item-label>
                      </q-item-section>
                      <q-item-section
                        side
                        class="text-grey-6 text-caption text-weight-light"
                        style="font-size: 0.7rem"
                      >
                        {{ act.time }}
                      </q-item-section>
                    </q-item>
                  </q-list>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Count Up Bar -->
    <section class="stats-bar q-py-lg bg-black-90 border-top-light border-bottom-light">
      <div class="container q-px-md">
        <div class="row q-col-gutter-lg justify-center text-center">
          <div class="col-4 col-sm-3" v-for="stat in keyMetrics" :key="stat.label">
            <div class="text-h4 text-weight-bold text-gradient-full-red">{{ stat.value }}</div>
            <div class="text-caption text-grey-5 text-uppercase q-mt-xs tracking-wider">
              {{ stat.label }}
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="q-py-xl container q-px-md">
      <div class="column items-center q-mb-xl text-center">
        <q-chip
          outline
          color="primary"
          text-color="white"
          icon="star"
          label="CORE FEATURES"
          class="q-mb-md"
        />
        <h2 class="text-h3 text-weight-bolder text-white q-my-none">
          Tailored Modules for Enterprise CRM
        </h2>
        <p class="text-subtitle1 text-grey-5 text-weight-light q-mt-sm" style="max-width: 600px">
          ApexCRM integrates all necessary customer tools, from pipelines to automated ticketing and
          real-time reports.
        </p>
      </div>

      <div class="row q-col-gutter-lg">
        <div class="col-12 col-sm-6 col-md-3" v-for="feat in crmFeatures" :key="feat.title">
          <div
            class="glass-card q-pa-lg text-center full-height column items-center justify-between"
          >
            <div class="column items-center">
              <q-avatar
                size="56px"
                color="primary-glow"
                text-color="primary"
                :icon="feat.icon"
                class="q-mb-md shadow-red"
              />
              <div class="text-h6 text-weight-bold text-white q-mb-sm">{{ feat.title }}</div>
              <p class="text-caption text-grey-5 text-weight-light">{{ feat.description }}</p>
            </div>
            <q-btn
              flat
              color="primary"
              label="Learn More"
              icon-right="chevron_right"
              class="text-weight-bold text-capitalize q-mt-md"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- Interactive Mini-CRM Widget (The Live Demo) -->
    <section id="demo" class="q-py-xl bg-black-90 border-top-light border-bottom-light">
      <div class="container q-px-md">
        <div class="row q-col-gutter-xl items-center">
          <div class="col-12 col-lg-5">
            <q-chip
              outline
              color="primary"
              text-color="white"
              icon="bolt"
              label="LIVE INTERACTIVE DEMO"
              class="q-mb-md"
            />
            <h2 class="text-h3 text-weight-bolder text-white q-mt-none q-mb-md">
              Test Drive Our Live CRM Platform
            </h2>
            <p class="text-subtitle1 text-grey-5 text-weight-light q-mb-lg">
              Experience the blazing speed of our customer database. Add a customer lead, modify
              their stage in the sales funnel, search the list instantly, or toggle status right in
              front of your eyes.
            </p>
            <div class="q-gutter-md q-mb-lg">
              <div class="row items-start q-gutter-sm">
                <q-icon name="check_circle" color="primary" size="20px" />
                <span class="text-subtitle2 text-grey-4 text-weight-light"
                  >Blazing-fast in-memory processing.</span
                >
              </div>
              <div class="row items-start q-gutter-sm">
                <q-icon name="check_circle" color="primary" size="20px" />
                <span class="text-subtitle2 text-grey-4 text-weight-light"
                  >Instant reactive state sync for multi-user collaboration.</span
                >
              </div>
              <div class="row items-start q-gutter-sm">
                <q-icon name="check_circle" color="primary" size="20px" />
                <span class="text-subtitle2 text-grey-4 text-weight-light"
                  >Dynamic color coding based on deal pipeline status.</span
                >
              </div>
            </div>
            <q-btn
              unelevated
              color="primary"
              label="Integrate Into Your Website"
              class="btn-premium text-weight-bold"
              style="border-radius: 8px"
            />
          </div>

          <div class="col-12 col-lg-7">
            <!-- The Mock CRM Widget Card -->
            <div class="glass-card border-gradient-red q-pa-md q-pa-sm-lg">
              <div class="row justify-between items-center q-mb-md q-col-gutter-sm">
                <div class="text-subtitle1 text-weight-bold text-white">
                  <q-icon name="people" color="primary" class="q-mr-xs" size="24px" />
                  Lead Management Board
                </div>
                <div class="row items-center q-gutter-sm">
                  <!-- Search input -->
                  <q-input
                    dark
                    dense
                    outlined
                    v-model="demoSearch"
                    placeholder="Search leads..."
                    class="bg-dark"
                    style="width: 180px"
                  >
                    <template v-slot:append>
                      <q-icon name="search" size="xs" color="grey-5" />
                    </template>
                  </q-input>
                </div>
              </div>

              <!-- Add New Lead Form -->
              <div class="q-pa-md rounded-borders bg-dark q-mb-md border-light">
                <div class="text-caption text-weight-bold text-primary q-mb-md">
                  ADD NEW LEAD IN REAL-TIME
                </div>
                <div class="row q-col-gutter-sm items-center">
                  <div class="col-12 col-sm-4">
                    <q-input
                      dark
                      dense
                      outlined
                      v-model="newLead.name"
                      label="Name"
                      color="primary"
                    />
                  </div>
                  <div class="col-12 col-sm-4">
                    <q-input
                      dark
                      dense
                      outlined
                      v-model="newLead.company"
                      label="Company"
                      color="primary"
                    />
                  </div>
                  <div class="col-12 col-sm-4">
                    <q-select
                      dark
                      dense
                      outlined
                      v-model="newLead.stage"
                      :options="stagesList"
                      label="Funnel Stage"
                      color="primary"
                    />
                  </div>
                  <div class="col-12 row justify-end q-mt-sm">
                    <q-btn
                      unelevated
                      dense
                      color="primary"
                      label="Insert Lead"
                      icon="add"
                      class="q-px-md text-weight-bold"
                      @click="addDemoLead"
                    />
                  </div>
                </div>
              </div>

              <!-- Leads Table -->
              <div class="leads-table-container">
                <div
                  class="row text-caption text-weight-bold text-grey-5 border-bottom q-pb-sm q-px-sm"
                >
                  <div class="col-4">NAME & COMPANY</div>
                  <div class="col-4 text-center">FUNNEL STAGE</div>
                  <div class="col-2 text-center">STATUS</div>
                  <div class="col-2 text-center">ACTION</div>
                </div>

                <div v-if="filteredLeads.length === 0" class="text-center text-grey-6 q-py-xl">
                  <q-icon name="people_outline" size="48px" class="q-mb-sm opacity-50" />
                  <div>No leads found matching your search.</div>
                </div>

                <div v-else class="leads-list">
                  <div
                    v-for="lead in filteredLeads"
                    :key="lead.id"
                    class="row items-center border-bottom q-py-sm q-px-sm lead-row"
                  >
                    <div class="col-4">
                      <div class="row items-center q-gutter-sm">
                        <q-avatar
                          size="28px"
                          color="primary"
                          text-color="white"
                          class="text-weight-bold text-caption font-mono"
                        >
                          {{ lead.name.charAt(0).toUpperCase() }}
                        </q-avatar>
                        <div>
                          <div class="text-subtitle2 text-weight-bold text-white lh-tight">
                            {{ lead.name }}
                          </div>
                          <div class="text-caption text-grey-5" style="font-size: 0.75rem">
                            {{ lead.company }}
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="col-4 text-center">
                      <q-btn-dropdown
                        dense
                        flat
                        :color="getStageColor(lead.stage)"
                        :label="lead.stage"
                        size="xs"
                        class="text-weight-bold"
                      >
                        <q-list dark style="min-width: 150px" class="bg-dark border-light">
                          <q-item
                            v-for="stg in stagesList"
                            :key="stg"
                            clickable
                            v-close-popup
                            @click="changeLeadStage(lead.id, stg)"
                            class="text-caption text-weight-medium"
                          >
                            <q-item-section>{{ stg }}</q-item-section>
                          </q-item>
                        </q-list>
                      </q-btn-dropdown>
                    </div>
                    <div class="col-2 text-center">
                      <q-toggle
                        dense
                        v-model="lead.active"
                        checked-icon="check"
                        unchecked-icon="clear"
                        color="positive"
                        @update:model-value="toggleLeadStatus(lead.name, lead.active)"
                      />
                    </div>
                    <div class="col-2 text-center">
                      <q-btn
                        flat
                        round
                        dense
                        color="negative"
                        size="sm"
                        icon="delete"
                        @click="deleteLead(lead.id)"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CRM ROI Calculator Section -->
    <section id="roi" class="q-py-xl container q-px-md">
      <div class="row q-col-gutter-xl items-center">
        <div class="col-12 col-lg-6 order-last order-lg-first">
          <!-- Calculator UI -->
          <div class="glass-card border-gradient-red q-pa-md q-pa-sm-lg">
            <div class="row items-center q-gutter-sm q-mb-lg border-bottom-red q-pb-md">
              <q-avatar color="primary" text-color="white" icon="calculate" size="40px" />
              <div>
                <div class="text-subtitle1 text-weight-bold text-white">
                  ROI & Time Savings Calculator
                </div>
                <div class="text-caption text-grey-5">
                  Estimate what automation can do for your business
                </div>
              </div>
            </div>

            <!-- Leads slider -->
            <div class="q-mb-md">
              <div class="row justify-between text-caption text-grey-4 q-mb-xs">
                <span>Number of Active Leads/Customers</span>
                <span class="text-weight-bold text-white">{{ calcLeads.toLocaleString() }}</span>
              </div>
              <q-slider
                v-model="calcLeads"
                :min="100"
                :max="10000"
                :step="100"
                color="primary"
                dark
              />
            </div>

            <!-- Hours slider -->
            <div class="q-mb-md">
              <div class="row justify-between text-caption text-grey-4 q-mb-xs">
                <span>Hours spent per lead/month (Manual tracking)</span>
                <span class="text-weight-bold text-white">{{ calcHours }} hrs</span>
              </div>
              <q-slider v-model="calcHours" :min="1" :max="20" :step="1" color="primary" dark />
            </div>

            <!-- Wage slider -->
            <div class="q-mb-xl">
              <div class="row justify-between text-caption text-grey-4 q-mb-xs">
                <span>Hourly wage per sales rep ($)</span>
                <span class="text-weight-bold text-white">${{ calcRate }}/hr</span>
              </div>
              <q-slider v-model="calcRate" :min="15" :max="150" :step="5" color="primary" dark />
            </div>

            <!-- Calculations Output Grid -->
            <div class="row q-col-gutter-md text-center">
              <div class="col-12 col-sm-4">
                <div class="bg-dark-card q-pa-md rounded-borders border-light">
                  <div class="text-caption text-grey-5">Monthly Hours Saved</div>
                  <div class="text-h5 text-weight-bold text-white q-mt-xs">
                    {{ totalHoursSaved.toLocaleString() }}h
                  </div>
                  <div class="text-caption text-grey-6">with 45% CRM automation</div>
                </div>
              </div>
              <div class="col-12 col-sm-4">
                <div class="bg-dark-card q-pa-md rounded-borders border-light">
                  <div class="text-caption text-grey-5">Monthly Revenue Saved</div>
                  <div class="text-h5 text-weight-bold text-primary q-mt-xs">
                    ${{ monthlySavings.toLocaleString() }}
                  </div>
                  <div class="text-caption text-grey-6">rep efficiency boost</div>
                </div>
              </div>
              <div class="col-12 col-sm-4">
                <div class="bg-dark-card q-pa-md rounded-borders border-light">
                  <div class="text-caption text-grey-5">Annual Savings</div>
                  <div class="text-h5 text-weight-bold text-gradient-full-red q-mt-xs">
                    ${{ annualSavings.toLocaleString() }}
                  </div>
                  <div class="text-caption text-grey-6">overall cost reduction</div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-12 col-lg-6">
          <q-chip
            outline
            color="primary"
            text-color="white"
            icon="trending_up"
            label="ROI PROJECTIONS"
            class="q-mb-md"
          />
          <h2 class="text-h3 text-weight-bolder text-white q-mt-none q-mb-md">
            Stop Wasting Hours on Manual Spreadsheets
          </h2>
          <p class="text-subtitle1 text-grey-5 text-weight-light q-mb-lg">
            Studies show that manual lead tracking costs businesses thousands in leaked leads,
            forgotten follow-ups, and repetitive data entry.
          </p>
          <div class="q-gutter-md q-mb-lg">
            <div class="row items-start q-gutter-sm">
              <q-avatar
                size="32px"
                color="primary-glow"
                text-color="primary"
                icon="timer"
                class="shadow-red"
              />
              <div class="col">
                <div class="text-subtitle2 text-white text-weight-bold">
                  Save 40%+ on admin tasks
                </div>
                <div class="text-caption text-grey-5">
                  Automate email sequences, lead logging, and task reminders.
                </div>
              </div>
            </div>
            <div class="row items-start q-gutter-sm">
              <q-avatar
                size="32px"
                color="primary-glow"
                text-color="primary"
                icon="trending_up"
                class="shadow-red"
              />
              <div class="col">
                <div class="text-subtitle2 text-white text-weight-bold">Recover leaky funnels</div>
                <div class="text-caption text-grey-5">
                  Get automated alerts whenever a high-value lead is idle for over 48 hours.
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Carousel Section -->
    <section id="testimonials" class="q-py-xl bg-black-90 border-top-light border-bottom-light">
      <div class="container q-px-md">
        <div class="column items-center q-mb-xl text-center">
          <q-chip
            outline
            color="primary"
            text-color="white"
            icon="rate_review"
            label="TESTIMONIALS"
            class="q-mb-md"
          />
          <h2 class="text-h3 text-weight-bolder text-white q-my-none">
            Trusted by Innovative Global Teams
          </h2>
          <p class="text-subtitle1 text-grey-5 text-weight-light q-mt-sm" style="max-width: 600px">
            Here is what our clients say about how ApexCRM reshaped their business workflow.
          </p>
        </div>

        <!-- Testimonial Cards Carousel -->
        <div class="row q-col-gutter-lg justify-center">
          <div class="col-12 col-md-4" v-for="test in testimonialsList" :key="test.name">
            <div class="glass-card q-pa-lg text-left full-height column justify-between">
              <div class="q-mb-md">
                <div class="row q-gutter-xs q-mb-sm">
                  <q-icon v-for="star in 5" :key="star" name="star" color="warning" size="18px" />
                </div>
                <p class="text-subtitle2 text-grey-4 text-weight-light italic">
                  "{{ test.feedback }}"
                </p>
              </div>
              <div class="row items-center q-gutter-sm">
                <q-avatar size="36px" color="grey-8" text-color="white">
                  <q-icon name="person" />
                </q-avatar>
                <div>
                  <div class="text-subtitle2 text-weight-bold text-white">{{ test.name }}</div>
                  <div class="text-caption text-grey-5" style="font-size: 0.75rem">
                    {{ test.role }}, {{ test.company }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact & Quote Form Section -->
    <section id="contact" class="q-py-xl container q-px-md">
      <div class="row q-col-gutter-xl items-center">
        <div class="col-12 col-md-6">
          <q-chip
            outline
            color="primary"
            text-color="white"
            icon="mail"
            label="GET IN TOUCH"
            class="q-mb-md"
          />
          <h2 class="text-h3 text-weight-bolder text-white q-mt-none q-mb-md">
            Let's Fuel Your Business Growth
          </h2>
          <p class="text-subtitle1 text-grey-5 text-weight-light q-mb-lg">
            Have questions about integrations, security, or enterprise volume pricing? Send us a
            message and our lead consultants will respond within 12 hours.
          </p>

          <div class="q-gutter-sm">
            <div class="row items-center q-gutter-sm">
              <q-icon name="location_on" color="primary" size="20px" />
              <span class="text-subtitle2 text-grey-4 text-weight-light"
                >742 Evergreen Terrace, Tech Sector, SF</span
              >
            </div>
            <div class="row items-center q-gutter-sm">
              <q-icon name="phone" color="primary" size="20px" />
              <span class="text-subtitle2 text-grey-4 text-weight-light">+1 (555) 019-2834</span>
            </div>
            <div class="row items-center q-gutter-sm">
              <q-icon name="email" color="primary" size="20px" />
              <span class="text-subtitle2 text-grey-4 text-weight-light">consult@apexcrm.com</span>
            </div>
          </div>
        </div>

        <div class="col-12 col-md-6">
          <!-- Glass form container -->
          <div class="glass-card q-pa-md q-pa-sm-lg">
            <div class="text-h6 text-weight-bold text-white q-mb-md">Schedule a Consultation</div>
            <q-form @submit.prevent="submitContactForm" class="q-gutter-md">
              <q-input
                dark
                outlined
                v-model="contactForm.name"
                label="Your Name"
                color="primary"
                :rules="[(val) => !!val || 'Name is required']"
              />
              <q-input
                dark
                outlined
                v-model="contactForm.email"
                type="email"
                label="Your Email"
                color="primary"
                :rules="[(val) => !!val || 'Email is required']"
              />
              <q-select
                dark
                outlined
                v-model="contactForm.companySize"
                :options="companySizes"
                label="Company Size"
                color="primary"
              />
              <q-input
                dark
                outlined
                v-model="contactForm.message"
                type="textarea"
                label="Your Message / Query"
                color="primary"
                rows="4"
              />

              <div class="row justify-end">
                <q-btn
                  unelevated
                  type="submit"
                  color="primary"
                  label="Send Request"
                  class="btn-premium text-weight-bold"
                  style="border-radius: 8px"
                />
              </div>
            </q-form>
          </div>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()

// Hero Stats Mockup
const previewStats = [
  { title: 'Deals Won Today', value: '$45,800', change: '+24%', trendUp: true },
  { title: 'New Leads', value: '184', change: '+8%', trendUp: true },
  { title: 'Avg. Cycle Time', value: '6.4 Days', change: '-12%', trendUp: true },
  { title: 'Lead Conv. Rate', value: '14.2%', change: '-1.5%', trendUp: false },
]

const pipelineStats = [
  { name: 'Lead Qualified', value: '$120,400', percent: 80 },
  { name: 'Demo Conducted', value: '$95,000', percent: 65 },
  { name: 'Proposal Sent', value: '$178,800', percent: 90 },
  { name: 'Negotiation', value: '$91,000', percent: 45 },
]

const recentActivities = [
  {
    id: 1,
    user: 'John Doe (Sales Manager)',
    details: 'Moved deal "Acme Tech" to Proposal stage',
    color: 'primary',
    icon: 'swap_horiz',
    time: '2m ago',
  },
  {
    id: 2,
    user: 'Sarah Connor',
    details: 'Added 5 new prospects from Web Form',
    color: 'positive',
    icon: 'person_add',
    time: '15m ago',
  },
  {
    id: 3,
    user: 'System Bot',
    details: 'Triggered auto-email sequence to 20 idle prospects',
    color: 'info',
    icon: 'smart_toy',
    time: '1h ago',
  },
]

const keyMetrics = [
  { value: '350M+', label: 'Contacts Managed' },
  { value: '15,000+', label: 'Active Teams' },
  { value: '99.99%', label: 'Platform Uptime' },
  { value: '4.8/5.0', label: 'Average Review' },
]

// Features Grid
const crmFeatures = [
  {
    icon: 'contacts',
    title: 'Unified Customer Database',
    description:
      'Maintain complete 360-degree history profiles of your customers including email correspondence, logs, and deals won.',
  },
  {
    icon: 'view_kanban',
    title: 'Sales Funnel Pipeline',
    description:
      'Visualize deal flow with clean pipelines. Drag, drop, and edit status to keep sales workflows predictable.',
  },
  {
    icon: 'auto_mode',
    title: 'Automation Engines',
    description:
      'Schedule instant email sequences, trigger Slack notifications, and assign customer support tasks automatically.',
  },
  {
    icon: 'insights',
    title: 'Deep Analytics Reporting',
    description:
      'Forecast revenue, review sales team activity logs, and isolate top leakages in your customer acquisition funnel.',
  },
]

// Interactive CRM Table Demo
const demoSearch = ref('')
const stagesList = ['Lead', 'Contacted', 'Proposal', 'Closed Won', 'Closed Lost']
const newLead = reactive({
  name: '',
  company: '',
  stage: 'Lead',
})

const demoLeads = ref([
  { id: 1, name: 'Alice Johnson', company: 'Alpha Group', stage: 'Closed Won', active: true },
  { id: 2, name: 'Bob Smith', company: 'Zenith Retail', stage: 'Proposal', active: true },
  { id: 3, name: 'Charlie Brown', company: 'Vortex Solutions', stage: 'Contacted', active: false },
  { id: 4, name: 'Diana Prince', company: 'Wayne Enterprises', stage: 'Lead', active: true },
])

const filteredLeads = computed(() => {
  const query = demoSearch.value.trim().toLowerCase()
  if (!query) return demoLeads.value
  return demoLeads.value.filter(
    (lead) =>
      lead.name.toLowerCase().includes(query) ||
      lead.company.toLowerCase().includes(query) ||
      lead.stage.toLowerCase().includes(query),
  )
})

function getStageColor(stage) {
  switch (stage) {
    case 'Closed Won':
      return 'positive'
    case 'Closed Lost':
      return 'negative'
    case 'Proposal':
      return 'warning'
    case 'Contacted':
      return 'info'
    default:
      return 'grey-5'
  }
}

function addDemoLead() {
  if (!newLead.name || !newLead.company) {
    $q.notify({
      message: 'Please fill in both Name and Company fields.',
      color: 'negative',
      icon: 'warning',
      position: 'top-right',
    })
    return
  }

  demoLeads.value.unshift({
    id: Date.now(),
    name: newLead.name,
    company: newLead.company,
    stage: newLead.stage,
    active: true,
  })

  $q.notify({
    message: `Lead "${newLead.name}" added successfully to the database!`,
    color: 'positive',
    icon: 'check',
    position: 'top-right',
  })

  // Reset form
  newLead.name = ''
  newLead.company = ''
  newLead.stage = 'Lead'
}

function changeLeadStage(id, newStage) {
  const lead = demoLeads.value.find((l) => l.id === id)
  if (lead) {
    lead.stage = newStage
    $q.notify({
      message: `Stage of "${lead.name}" updated to ${newStage}`,
      color: 'info',
      icon: 'sync',
      position: 'top-right',
    })
  }
}

function toggleLeadStatus(name, isActive) {
  $q.notify({
    message: `Lead "${name}" is now marked as ${isActive ? 'Active' : 'Inactive'}`,
    color: isActive ? 'positive' : 'grey-7',
    icon: isActive ? 'check' : 'power_settings_new',
    position: 'top-right',
  })
}

function deleteLead(id) {
  const index = demoLeads.value.findIndex((l) => l.id === id)
  if (index !== -1) {
    const deletedName = demoLeads.value[index].name
    demoLeads.value.splice(index, 1)
    $q.notify({
      message: `Lead "${deletedName}" removed from memory.`,
      color: 'negative',
      icon: 'delete',
      position: 'top-right',
    })
  }
}

// ROI Calculator Sliders
const calcLeads = ref(1500)
const calcHours = ref(6)
const calcRate = ref(45)

const totalHoursSaved = computed(() => {
  // Manual hours spent = leads * average hours per month
  // CRM automation reduces hours spent on tracking/admin tasks by 45%
  return Math.round(calcLeads.value * calcHours.value * 0.45)
})

const monthlySavings = computed(() => {
  return totalHoursSaved.value * calcRate.value
})

const annualSavings = computed(() => {
  return monthlySavings.value * 12
})

// Testimonials
const testimonialsList = [
  {
    feedback:
      'ApexCRM literally saved our sales team from spreadsheet hell. The dynamic pipeline and simple user status filters doubled our deals won within a single quarter.',
    name: 'Erlich Bachman',
    role: 'CEO',
    company: 'Aviato',
  },
  {
    feedback:
      'We migrated 10,000 customer profiles seamlessly. The automated email triggers alone save each agent around 12 hours a week. Very highly recommended.',
    name: 'Monica Hall',
    role: 'COO',
    company: 'Raviga',
  },
  {
    feedback:
      'The micro-interactions are super snappy and the customized black-red theme fits our developer-first branding perfectly. Incredible platform speed!',
    name: 'Richard Hendricks',
    role: 'Founder',
    company: 'Pied Piper',
  },
]

// Contact Form
const contactForm = reactive({
  name: '',
  email: '',
  companySize: '10-49 Employees',
  message: '',
})

const companySizes = ['1-9 Employees', '10-49 Employees', '50-249 Employees', '250+ Employees']

function submitContactForm() {
  $q.notify({
    message: `Thank you ${contactForm.name}! Our senior consultant will contact you at ${contactForm.email} shortly.`,
    color: 'positive',
    icon: 'mail',
    position: 'top-right',
    timeout: 3500,
  })

  // Reset Form
  contactForm.name = ''
  contactForm.email = ''
  contactForm.companySize = '10-49 Employees'
  contactForm.message = ''
}

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}
</script>

<style lang="scss">
.hero-section {
  padding-top: 100px;
}

.hero-badge {
  background: rgba(217, 4, 41, 0.1);
  border: 1px solid rgba(217, 4, 41, 0.3);
  border-radius: 50px;
  color: #ef233c;
}

.bg-glow {
  background: radial-gradient(circle, #d90429 0%, transparent 70%);
}

.bg-dark-card {
  background: rgba(15, 15, 18, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.border-light {
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 8px;
}

.border-bottom {
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.progress-bar-container {
  height: 6px;
  border-radius: 3px;
  overflow: hidden;
  width: 100%;
}

.progress-bar {
  height: 100%;
  border-radius: 3px;
}

.min-width-auto {
  min-width: auto;
}

.bg-black-90 {
  background-color: #050507;
}

.border-top-light {
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.border-bottom-light {
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.primary-glow {
  background: rgba(217, 4, 41, 0.15) !important;
}

.border-gradient-red {
  border: 1px solid rgba(217, 4, 41, 0.25);
  box-shadow: 0 4px 20px rgba(217, 4, 41, 0.04);
}

.leads-list {
  max-height: 250px;
  overflow-y: auto;
}

.lead-row {
  transition: background-color 0.2s ease;
  &:hover {
    background-color: rgba(255, 255, 255, 0.02);
  }
}

.leads-table-container {
  overflow-x: auto;
  min-width: 450px;
}

.lh-tight {
  line-height: 1.25;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  display: inline-block;
  &.bg-red {
    background-color: #d90429;
  }
}

.border-gradient {
  border: 1px solid rgba(255, 255, 255, 0.08);
}
</style>
