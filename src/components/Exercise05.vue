<template>
    <div>
        <p>Gender: {{ gender }}</p>
        <input v-model="gender" value="male" type="radio">Male
        <input v-model="gender" value="female" type="radio">Female
        <input v-model="gender" value="other" type="radio">Other
    </div>
</template>

<script setup>
import { ref } from 'vue';
    const gender = ref("male");
</script>

<style>

</style>