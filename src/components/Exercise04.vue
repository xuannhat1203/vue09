<template>
    <div>
        <p>Complete: {{ job }}%</p>
        <input type="range" v-model="job" min="0" max="100" />
    </div>
</template>

<script setup>
import { ref } from 'vue';
const job = ref(30);
</script>

<style>
</style>
