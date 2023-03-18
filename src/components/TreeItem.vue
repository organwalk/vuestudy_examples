<script setup>
import { ref, computed ,defineProps} from 'vue'

const props = defineProps({
  model: Object
})

const isOpen = ref(false)
const isFolder = computed(() => {
  return props.model.children && props.model.children.length
})

const children = ref(props.model.children)

function toggle() {
  isOpen.value = !isOpen.value
}

function changeType() {
  if (!isFolder.value) {
    children.value= []
    addChild()
    isOpen.value = true
  }
}

function addChild() {
  children.value.push({ name: 'new stuff' })
}
</script>

<template>
  <li>
    <div
      :class="{ bold: isFolder }"
      @click="toggle"
      @dblclick="changeType">
      {{ model.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <!--
        一个可以通过其“name”选项递归渲染自己的组件，
        (如果使用单文件组件，则从文件名推断)
      -->
      <TreeItem
        class="item"
        v-for="model in model.children" :key="model.id"
        :model="model">
      </TreeItem>
      <li class="add" @click="addChild">+</li>
    </ul>
  </li>
</template>