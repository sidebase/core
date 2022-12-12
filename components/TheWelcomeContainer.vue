<script setup lang="ts">
// eslint-disable-next-line @typescript-eslint/no-unused-vars
interface HealthCheckData {
  status: string;
  time: Date;
  startupTime: Date;
  nuxtAppVersion: string;
}

const { data: healthCheckData, refresh } = await useFetch('/api/healthz')

let refreshDataInterval: null | ReturnType<typeof setInterval> = null
let lastRefreshedAt = new Date()

onMounted(() => {
  refreshDataInterval = setInterval(() => {
    lastRefreshedAt = new Date()
    return refresh()
  }, 2000)
})

onBeforeUnmount(() => {
  if (refreshDataInterval) {
    clearInterval(refreshDataInterval)
  }
})
</script>

<template>
  <TheWelcome :last-refreshed-at="lastRefreshedAt" :health-check-data="(healthCheckData as HealthCheckData | null)" />
</template>
