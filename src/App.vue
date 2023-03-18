<template>
  <div>
    <HelloWorld></HelloWorld>
    <HandingInput></HandingInput>
    <AttributeBindings></AttributeBindings>
    <Conditionals_And_Loops></Conditionals_And_Loops>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import HandingInput from './components/Handing-Input.vue';
import AttributeBindings from './components/Attribute-Bindings.vue';
import Conditionals_And_Loops from './components/Conditionals_And_Loops.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    HandingInput,
    AttributeBindings,
    Conditionals_And_Loops,
  }
}
</script>

<style>

</style>
