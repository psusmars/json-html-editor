<template>
  <v-container class="fill-height ">

    <v-responsive class="fill-height ">
      <v-container class="text-center">

        <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>
        <h1 class="text-h2 font-weight-bold">J2H2J Editor</h1>
    </v-container>
      <div class="text-body-1 mb-4">To use this application</div>
      <InputArea/>
      <v-button @click=""></v-button>


      <div class="py-14" />

      
    </v-responsive>
  </v-container>
</template>

<script lang="ts" setup>
import { store } from '@/store.ts'
import InputArea from './InputArea.vue';

const loadData = () => {
  
}
</script>