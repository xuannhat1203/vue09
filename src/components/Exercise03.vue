<template>
   <div>
        <p>Date of birth: {{ date }}</p>
        <input type="date" v-model="date">
   </div>
</template>

<script setup>
import { ref } from 'vue';

    const date = ref("2024-10-1");
</script>

<style>

</style>