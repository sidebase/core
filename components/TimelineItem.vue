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
    <div class="flex flex-start items-center pt-3">
      <div :class="borderColor" class="-ml-2 mr-3 h-4 w-4 rounded-full border-2 bg-white"></div>
      <h4 class="mb-[1px] font-semibold text-gray-800">{{ title }}</h4>
    </div>
    <div v-if="content" class="ml-[21px]">
      <p class="text-gray-500 text-sm">{{ content }}</p>
    </div>
  </li>
</template>
