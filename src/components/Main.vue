<template>
  <v-container class="fill-height ">

    <v-responsive class="fill-height ">
      <v-container class="text-center">

        <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>
        <h1 class="text-h2 font-weight-bold">J2H2J Editor</h1>
      </v-container>
      <div class="text-body-1 mb-4">To use this application</div>
      <v-textarea :rules="[isValidJSON]" @update:model-value="loadData" v-model="inputData"
        label="Paste your JSON here..."></v-textarea>
      <v-btn :disabled="!canLoad" @click="loadData">
        Load
      </v-btn>


      <div class="py-14" />


    </v-responsive>
  </v-container>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const inputData = ref('');
const canLoad = ref(false);

const isValidJSON = (v: string) => {
  try {
    JSON.parse(v);
    return true;
  } catch (e) {
    return "Invalid JSON"
  }
}
const loadData = (inputValue: string) => canLoad.value = isValidJSON(inputValue) === true
</script>