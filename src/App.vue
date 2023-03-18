<template>
  <div>
    <HelloWorld></HelloWorld>
    <HandingInput></HandingInput>
    <AttributeBindings></AttributeBindings>
    <Conditionals_And_Loops></Conditionals_And_Loops>
    <FormBindings></FormBindings>
    <TodoItem v-for="item in groceryList" :todo="item" :key="item.id"></TodoItem><hr/>
    <Markdown_Test></Markdown_Test>
    <Fetching_data></Fetching_data><hr/>
    <div>
      <form id="search">
        Search <input name="query" v-model="searchQuery">
      </form>
      <Grid_Test
        :data="gridData"
        :columns="gridColumns"
        :filter-key="searchQuery">
      </Grid_Test>
    </div><hr/>
    <ul>
      <TreeItem class="item" :model="treeData"></TreeItem>
    </ul><hr/>
  <div style="width:500px">
    <svg width="200" height="200">
    <PolyGraph :stats="stats"></PolyGraph>
    </svg>
    <!-- 控件 -->
    <div v-for="stat in stats" :key="stat" style="width: 300px;">
    <label>{{stat.label}}</label>
    <input type="range" v-model="stat.value" min="0" max="100">
    <span>{{stat.value}}</span>
    <button @click="remove(stat)" class="remove">X</button>
    </div>
    <form id="add">
    <input name="newlabel" v-model="newLabel">
    <button @click="add">Add a Stat</button>
    </form>
    <pre id="raw">{{ stats }}</pre>
  </div><hr/>
  <div>
    <button id="show-modal" @click="showModal = true">Show Modal</button>
    <Teleport to="body">
      <!-- 使用这个 modal 组件，传入 prop -->
      <Modal_Test :show="showModal" @close="showModal = false">
        <template #header>
          <h3>custom header</h3>
        </template>
      </Modal_Test>
    </Teleport>
  </div><hr/>
  <List_Transition/><hr/>
  <TodoMvc/><hr/>
  <h1>7GUIs</h1>
  <Counter_Test/><hr/>
  <temperature_converter/><hr/>
  <FightBooker/><hr/>
  <CRUD_Test/><hr/>
  <CircleDrawer/><hr/>
  </div>
</template>

<script setup>
import { ref,reactive } from 'vue'
import HelloWorld from './components/HelloWorld.vue';
import HandingInput from './components/Handing-Input.vue';
import AttributeBindings from './components/Attribute-Bindings.vue';
import Conditionals_And_Loops from './components/Conditionals_And_Loops.vue';
import FormBindings from './components/Form-Bindings.vue';
import TodoItem from './components/TodoItem.vue';
import Markdown_Test from './components/Markdown_Test.vue';
import Fetching_data from './components/Fetching_data.vue';
import Grid_Test from './components/Grid_Test.vue';
import TreeItem from './components/TreeItem.vue';
import PolyGraph from './components/PolyGraph.vue';
import Modal_Test from './components/Modal_Test.vue';
import List_Transition from './components/List_Transition.vue';
import TodoMvc from './components/TodoMVC.vue'
import Counter_Test from './7GUIs/Counter_Test.vue';
import temperature_converter from './7GUIs/temperature_converter.vue';
import FightBooker from './7GUIs/Fight_Booker.vue'
import CRUD_Test from './7GUIs/CRUD_Test.vue';
import CircleDrawer from './7GUIs/Circle-Drawer.vue';

const groceryList = ref([
  { id: 0, text: 'Vegetables' },
  { id: 1, text: 'Cheese' },
  { id: 2, text: 'Whatever else humans are supposed to eat' }
])

const searchQuery = ref('')
const gridColumns = ['name', 'power']
const gridData = [
  { name: 'Chuck Norris', power: Infinity },
  { name: 'Bruce Lee', power: 9000 },
  { name: 'Jackie Chan', power: 7000 },
  { name: 'Jet Li', power: 8000 }
]

const treeData = ref({
  name: 'My Tree',
  children: [
    { name: 'hello' },
    { name: 'world' },
    {
      name: 'child folder',
      children: [
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }]
        },
        { name: 'hello' },
        { name: 'world' },
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }]
        }
      ]
    }
  ]
})

const newLabel = ref('')
const stats = reactive([
  { label: 'A', value: 100 },
  { label: 'B', value: 100 },
  { label: 'C', value: 100 },
  { label: 'D', value: 100 },
  { label: 'E', value: 100 },
  { label: 'F', value: 100 }
])

function add(e) {
  e.preventDefault()
  if (!newLabel.value) return
  stats.push({
    label: newLabel.value,
    value: 100
  })
  newLabel.value = ''
}

function remove(stat) {
  if (stats.length > 3) {
    stats.splice(stats.indexOf(stat), 1)
  } else {
    alert("Can't delete more!")
  }
}

const showModal = ref(false)
</script>

<style>
.item {
  cursor: pointer;
  line-height: 1.5;
}
.bold {
  font-weight: bold;
}
polygon {
  fill: #42b983;
  opacity: 0.75;
}

circle {
  fill: transparent;
  stroke: #999;
}

text {
  font-size: 10px;
  fill: #666;
}

label {
  display: inline-block;
  margin-left: 10px;
  width: 20px;
}

#raw {
  position: absolute;
  left: 300px;
  margin-top: -500px;
}
</style>
