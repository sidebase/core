<script setup lang="ts">
import type { PropType } from 'vue'
import { computed } from 'vue'
import { NTimeline, NTimelineItem } from 'naive-ui'

interface HealthCheckData {
  status: string;
  time: Date;
  startupTime: Date;
  nuxtAppVersion: string;
}

const props = defineProps({
  healthCheckData: {
    type: Object as PropType<HealthCheckData | null>,
    required: true
  },
  lastRefreshedAt: {
    type: Object as PropType<Date>,
    required: true
  }
})

const parsedHealthCheckData = computed(() => {
  if (!props.healthCheckData) {
    return null
  }

  const data = props.healthCheckData
  return {
    ...data,
    time: new Date(data.time),
    startupTime: new Date(data.startupTime)
  }
})
</script>

<template>
  <div class="TheWelcome">
    <Head>
      <Title>sidebase</Title>
    </Head>
    <div class="container">
      <h1 class="text-4xl">
        Welcome to <a href="https://github.com/sidebase/sidebase" target="_blank" class="GradientText">sidebase</a>!
      </h1>
      <p><a href="https://github.com/sidebase/sidebase" target="_blank" class="GradientText">sidebase</a> is the productive Nuxt 3 stack. It comes with batteries included: Tailwind, Naive UI, Testing, DB ORM, API examples, authentication module, session module, ... are all there.</p>
      <p class="my-4">
        The data you see below is fetched from an API that is connected to a running database.
      </p>
      <ol v-if="parsedHealthCheckData" class="TimeLine">
        <TimelineItem border-color="border-green-500" :title="`Server v${parsedHealthCheckData.nuxtAppVersion} initialized`" />
        <TimelineItem border-color="border-green-500" :title="`Started at ${parsedHealthCheckData.startupTime.toLocaleString()}`" />
        <TimelineItem border-color="border-blue-500" title="Healthy" :content="`Last checked at ${parsedHealthCheckData.time.toLocaleString()}`" />
      </ol>
      <ol v-else class="TimeLine">
        <TimelineItem
          border-color="border-red-500"
          title="Server initialization failed"
          :content="`Last checked at ${lastRefreshedAt?.toLocaleString() || 'N/A'}`"
        />
      </ol>
      <p class="my-4">
        The above status is updated every couple seconds. DB, App and Server all start with a single command: <b>npm run dev</b>.
      </p>
      <p class="my-4">
        Remove this page by replacing <b>&lt;TheWelcomeContainer /&gt;</b> in <b>app.vue</b> with your own code.
      </p>
    </div>
  </div>
</template>

<style>
.TheWelcome {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  display: flex;
  flex-direction: column;
  width: 66.666667%;
  max-width: 32rem;
}

.text-4xl {
  font-size: 2.25rem;
  line-height: 2.5rem;
}

.my-4 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.TimeLine {
  border-left-width: 1px;
  border-color: #D1D5DB;

}

.GradientText {
  background: linear-gradient(to right, #5eaa95 10%, #12a87b 40%, #0FCF97 60%, #5eaa95 90%);
  background-size: 200% auto;

  color: #000;
  background-clip: text;
  text-fill-color: transparent;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;

  animation: shine 1s linear infinite;
@keyframes shine {
  to {
    background-position: 200% center;
  }
}
}
</style>
