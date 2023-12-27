<template>
  <v-textarea :model-value="modelValue" @update:model-value="$emit('update:modelValue', $event)"
    :label="label"></v-textarea>
</template>
<script setup lang="ts">
defineEmits(['update:modelValue'])
defineProps({
  modelValue: {
    type: String,
    required: true
  },
  label: {
    type: String,
    default: 'Label'
  }
})

</script>

<style scoped>
/* Component styles go here */
</style>
