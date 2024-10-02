<template>
    <div>
      <div>
        <input type="color" id="head" name="head" v-model="code" />
        <p>Color Code: {{ code }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  const code = ref("#e66465"); 
  </script>
  
  <style></style>
    