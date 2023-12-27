<template>
  <a-textarea v-model:value="value" placehold="Paste your JSON here..." :rows="6" a-textarea/>
</template>
<script setup lang="ts">
import {ref} from 'vue'
const value  = ref('')

export default {
  name: 'InputArea',
}
</script>

<style scoped>
/* Component styles go here */
</style>
