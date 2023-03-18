<template>
  <div>
    <HelloWorld></HelloWorld>
    <HandingInput></HandingInput>
    <AttributeBindings></AttributeBindings>
    <Conditionals_And_Loops></Conditionals_And_Loops>
    <FormBindings></FormBindings>
    <TodoItem v-for="item in groceryList" :todo="item" :key="item.id"></TodoItem>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue';
import HandingInput from './components/Handing-Input.vue';
import AttributeBindings from './components/Attribute-Bindings.vue';
import Conditionals_And_Loops from './components/Conditionals_And_Loops.vue';
import FormBindings from './components/Form-Bindings.vue';
import TodoItem from './components/TodoItem.vue';

const groceryList = ref([
  { id: 0, text: 'Vegetables' },
  { id: 1, text: 'Cheese' },
  { id: 2, text: 'Whatever else humans are supposed to eat' }
])
</script>

<style>

</style>
