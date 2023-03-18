<template>
    <div>
        <p>
            <span :title="message">
                Hover your mouse over me for a few seconds to see my dynamically bound title!
            </span>
        </p>

        <p :class="{ red: isRed }" @click="toggleRed">
            This should be red... but click me to toggle it.
        </p>

        <p :style=" { color }" @click="toggleColor">
            This should be green, and should toggle between green and blue on click.
        </p>
    </div><hr/>
</template>

<script setup>
    import {ref} from 'vue'

    const message = ref('Hello World')
    const isRed = ref(true)
    const color = ref('green')

    function toggleRed(){
        isRed.value = !isRed.value
    }

    function toggleColor(){
        color.value = color.value === 'green' ? 'blue' :'green'
    }
</script>

<style>
.red{
    color: red;
}
</style>