<script setup lang="ts">
defineProps({
  title: {
    type: String,
    required: true
  },
  borderColor: {
    type: String,
    default: 'border-blue-500'
  },
  content: {
    type: String,
    default: undefined
  }
})
</script>

<template>
  <li>
    <div class="top">
      <div :class="borderColor" class="icon" />
      <h4 class="title">{{ title }}</h4>
    </div>
    <div v-if="content" style="margin-left: 21px">
      <p class="content">{{ content }}</p>
    </div>
  </li>
</template>

<style scoped>
.top {
  display: flex;
  padding-top: 0.75rem;
  align-items: center;
}

.icon {
  margin-right: 0.75rem;
  margin-left: -0.5rem;
  background-color: #ffffff;
  width: 1rem;
  height: 1rem;
  border-radius: 9999px;
  border-width: 2px;
}

.border-blue-500 {
  border-color: #3B82F6;
}

.border-green-500 {
  border-color: #10B981;
}

.border-red-500 {
  border-color: #EF4444;
}

.title {
  color: #1F2937;
  font-weight: 600;
  margin-bottom: 1px;
}

.content {
  color: #6B7280;
  font-size: 0.875rem;
  line-height: 1.25rem;
}
</style>
