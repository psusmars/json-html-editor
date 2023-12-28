<template>
  <v-container class="fill-height ">

    <v-responsive class="fill-height ">
      <v-container class="text-center">

        <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>
        <h1 class="text-h2 font-weight-bold">J2H2J Editor</h1>
      </v-container>
      <div class="stack">
        <div class="full-width text-body-1">To use this application</div>
        <v-textarea class="full-width" :rules="[isValidJSON]" @paste="loadData" v-model="inputData"
          label="Paste your JSON here..."></v-textarea>
        <v-btn :disabled="!canLoad" @click="loadData">
          Load
        </v-btn>
        <v-combobox v-model="selectedKey" :disabled="jsonKeys.length <= 0" class="full-width"
          label="Select HTML Key to Adjust" :items="jsonKeys"></v-combobox>
        <v-textarea :focused="!!selectedKey" class="full-width" :disabled="!selectedKey" v-model="loadedHtml"
          label="The HTML to Edit"></v-textarea>
      </div>

    </v-responsive>
  </v-container>
</template>

<script lang="ts" setup>
import get from 'lodash/get';
import { ref, watchEffect, computed } from 'vue';

const isValidJSON = (v: string) => {
  try {
    JSON.parse(v);
    return true;
  } catch (e) {
    return "Invalid JSON"
  }
}

const inputData = ref('');
const jsonKeys = ref<Array<string>>([]);
const selectedKey = ref('');
const canLoad = computed(() => isValidJSON(inputData.value) === true);
const loadedJSON = computed(() => canLoad.value ? JSON.parse(inputData.value) : '');
const loadedHtml = ref('');
// watch(() => ({key: selectedKey.value, json: loadedJSON.value}), (newVal) => {
//   loadedHtml.value = newVal.json ? get(newVal.json, newVal.key) : ''
// }, {deep: true});
watchEffect(() => {
  loadedHtml.value = loadedJSON.value ? get(loadedJSON.value, selectedKey.value) : ''
});
const collectKeys = (obj: any, parentKey = '') => {
  let keys: Array<string> = [];
  Object.keys(obj).forEach((key) => {
    const currentKey = parentKey ? `${parentKey}.${key}` : key;
    if (typeof obj[key] === 'object' && !Array.isArray(obj[key])) {
      keys = [...keys, ...collectKeys(obj[key], currentKey)];
    } else if (typeof obj[key] === 'string') {
      keys.push(currentKey);
    }
  })
  return keys
}

const loadData = () => {
  selectedKey.value = '';
  jsonKeys.value = collectKeys(JSON.parse(inputData.value));
}
</script>

<style scoped>
.full-width {
  width: 100%;
}

.stack {
  width: 100%;
  display: flex;
  flex-direction: column;
  -moz-box-pack: center;
  justify-content: center;
  -moz-box-align: center;
  align-items: center;
  gap: 16px;
}
</style>