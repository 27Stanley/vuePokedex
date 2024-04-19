<script setup>
import { defineProps } from "vue";

defineProps({
  name: {
    type: String,
    required: true,
  },
  number: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <li>{{ number }} - {{ name }}</li>
</template>

<style></style>
