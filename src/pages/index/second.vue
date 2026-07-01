<template>
  <q-page class="q-pa-lg flex flex-center bg-dark text-white">
    <div class="glass-card q-pa-xl text-center shadow-red animate-fade-in" style="max-width: 500px">
      <q-avatar
        size="72px"
        color="primary-glow"
        text-color="primary"
        icon="settings"
        class="q-mb-md shadow-red animate-spin"
      />
      <h3 class="text-h4 text-weight-bolder text-white q-mt-none q-mb-md">CRM Console Settings</h3>
      <p class="text-subtitle2 text-grey-5 text-weight-light q-mb-xl">
        This is a mock dashboard sub-page demonstrating system settings, API keys, and workspace
        profile parameters.
      </p>

      <div class="row q-gutter-md justify-center">
        <q-btn
          unelevated
          color="primary"
          to="/"
          label="Return to Home"
          icon="arrow_back"
          class="btn-premium text-weight-bold"
          style="border-radius: 8px"
        />
        <q-btn
          outline
          color="white"
          label="Configure API"
          class="text-weight-bold"
          style="border-radius: 8px"
          @click="showApiNotification"
        />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { useQuasar } from 'quasar'

const $q = useQuasar()

function showApiNotification() {
  $q.notify({
    message: 'API configuration is locked in demo mode.',
    color: 'warning',
    icon: 'lock',
    position: 'top-right',
  })
}
</script>

<style lang="scss" scoped>
.animate-spin {
  animation: spin 12s linear infinite;
}

.animate-fade-in {
  animation: fadeIn 0.8s ease-out;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
