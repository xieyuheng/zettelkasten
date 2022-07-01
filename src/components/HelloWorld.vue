<script setup lang="ts">
import { ref } from "vue"

defineProps<{ message: string }>()

const count = ref(0)
</script>

<template>
  <h1>{{ message }}</h1>
</template>
