<template>
  <div v-if="error" class="alert alert-danger mt-4">{{ error }}</div>
  <div v-else-if="result !== null" class="alert alert-success mt-4">Le resulat est: {{ result }}</div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  result: Number,
  error: String
});

</script>

<style scoped>

</style>
