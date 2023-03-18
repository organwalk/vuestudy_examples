<template>
    <li>{{ todo.text }}</li>
</template>

<script setup>
import { defineProps } from '@vue/runtime-core';
    defineProps({
        todo:Object
    })

</script>