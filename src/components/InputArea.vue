<template>
  <v-textarea v-model:model-value="value" label="Paste your JSON here..."></v-textarea>
</template>
<script setup lang="ts">
import {ref} from 'vue'
const value  = ref('')

</script>

<style scoped>
/* Component styles go here */
</style>
