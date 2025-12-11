<script setup>
import {ref, onMounted} from 'vue';

let count = ref(0);


function increment() {
    count.value++;
}

onMounted(() => {
    console.log("ApiDemo mounted");
});

</script>


<template>

    <button @click="increment">count is: {{ count }}</button>
</template>


<style scoped>

</style>