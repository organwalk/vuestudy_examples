<template>
    <h1>{{ message }}</h1><hr/>
</template>

<script setup>
    import { ref } from "vue";
    const message = ref('Hello World');

</script>