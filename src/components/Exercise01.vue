<template>
    <div>
        <input v-model="inputValue" type="text">
        <p>Value: {{ inputValue }}</p>
    </div>
</template>

<script setup>
import { ref } from 'vue';

    const inputValue = ref("");
</script>

<style>

</style>