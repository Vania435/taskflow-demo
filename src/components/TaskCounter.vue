<script setup>
// Додаткове завдання 3: лічильник отримує число завдань через Props
defineProps({
  label: { type: String, required: true },
  value: { type: Number, required: true },
  accent: { type: String, default: 'default' },
})
</script>

<template>
  <div class="tf3-stat" :class="`tf3-stat--${accent}`">
    <span class="tf3-stat-label">{{ label }}</span>
    <strong>{{ value }}</strong>
  </div>
</template>
