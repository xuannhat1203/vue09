<template>
    <div>
        <p>Hobbies: {{ hobbies }} </p>
        <input v-model="hobbies" value="Football" type="checkbox">Football
        <input v-model="hobbies"  value="Badminton" type="checkbox">Badminton
        <input v-model="hobbies"  value="Swim" type="checkbox">Swim
        <input v-model="hobbies"  value="Tennis" type="checkbox">Tennis
    </div>
</template>
<script setup>
import { ref } from 'vue';
    const hobbies = ref([]);
</script>

<style>

</style>