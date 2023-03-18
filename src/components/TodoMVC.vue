<script setup>
import { ref, computed, watchEffect } from 'vue'

const STORAGE_KEY = 'vue-todomvc' //用于在本地存储中存储待办事项列表的数据。

const filters = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed)
}   //用于定义不同的筛选条件及其对应的过滤函数。

// 状态
const todos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'))
//创建一个响应式引用 todos，初始值为从本地存储中读取的待办事项列表数据
//如果本地存储中没有数据，则初始值为一个空数组
const visibility = ref('all')
//创建一个响应式引用 visibility，初始值为字符串 'all'，表示当前的筛选条件为“全部”。
const editedTodo = ref()
//创建一个响应式引用 editedTodo，用于表示当前正在编辑中的待办事项。

// 获取的状态
const filteredTodos = computed(() => filters[visibility.value](todos.value))
//创建一个计算属性 filteredTodos，用于根据当前筛选条件过滤待办事项列表。
const remaining = computed(() => filters.active(todos.value).length)
//创建一个计算属性 remaining，用于计算未完成的待办事项数量。

// 处理路由
window.addEventListener('hashchange', onHashChange)
onHashChange()//监听路由变化，当路由变化时，根据路由切换当前的筛选条件。

// 状态持久化
watchEffect(() => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value))
})//监听待办事项列表的变化，当待办事项列表发生变化时，将新的列表数据存储到本地存储中。

//用于标记所有待办事项为已完成或未完成。
function toggleAll(e) {
  todos.value.forEach((todo) => (todo.completed = e.target.checked))
}
//用于添加一个新的待办事项
function addTodo(e) {
  const value = e.target.value.trim()
  if (value) {
    todos.value.push({
      id: Date.now(),
      title: value,
      completed: false
    })
    e.target.value = ''
  }
}
//用于删除一个待办事项
function removeTodo(todo) {
  todos.value.splice(todos.value.indexOf(todo), 1)
}
//用于开始编辑一个待办事项。
let beforeEditCache = ''
function editTodo(todo) {
  beforeEditCache = todo.title
  editedTodo.value = todo
}
//用于取消编辑一个待办事项。
function cancelEdit(todo) {
  editedTodo.value = null
  todo.title = beforeEditCache
}
//用于取消编辑一个待办事项。
function doneEdit(todo) {
  if (editedTodo.value) {
    editedTodo.value = null
    todo.title = todo.title.trim()
    if (!todo.title) removeTodo(todo)
  }
}
//用于删除所有已完成的待办事项。
function removeCompleted() {
  todos.value = filters.active(todos.value)
}

function onHashChange() {
  const route = window.location.hash.replace(/#\/?/, '')
  if (filters[route]) {
    visibility.value = route
  } else {
    window.location.hash = ''
    visibility.value = 'all'
  }
}
</script>

<template>
    <section class="todoapp">
      <header class="header">
        <h1>todos</h1>
        <input
          class="new-todo"
          autofocus
          placeholder="What needs to be done?"
          @keyup.enter="addTodo"
        >
      </header>
      <section class="main" v-show="todos.length">
        <input
          id="toggle-all"
          class="toggle-all"
          type="checkbox"
          :checked="remaining === 0"
          @change="toggleAll"
        >
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list">
          <li
            v-for="todo in filteredTodos"
            class="todo"
            :key="todo.id"
            :class="{ completed: todo.completed, editing: todo === editedTodo }"
          >
            <div class="view">
              <input class="toggle" type="checkbox" v-model="todo.completed">
              <label @dblclick="editTodo(todo)">{{ todo.title }}</label>
              <button class="destroy" @click="removeTodo(todo)"></button>
            </div>
            <input
              v-if="todo === editedTodo"
              class="edit"
              type="text"
              v-model="todo.title"
              @vnode-mounted="({ el }) => el.focus()"
              @blur="doneEdit(todo)"
              @keyup.enter="doneEdit(todo)"
              @keyup.escape="cancelEdit(todo)"
            >
          </li>
        </ul>
      </section>
      <footer class="footer" v-show="todos.length">
        <span class="todo-count">
          <strong>{{ remaining }}</strong>
          <span>{{ remaining === 1 ? ' item' : ' items' }} left</span>
        </span>
        <ul class="filters">
          <li>
            <a href="#/all" :class="{ selected: visibility === 'all' }">All</a>
          </li>
          <li>
            <a href="#/active" :class="{ selected: visibility === 'active' }">Active</a>
          </li>
          <li>
            <a href="#/completed" :class="{ selected: visibility === 'completed' }">Completed</a>
          </li>
        </ul>
        <button class="clear-completed" @click="removeCompleted" v-show="todos.length > remaining">
          Clear completed
        </button>
      </footer>
    </section>
  </template>

<style>
@import "https://unpkg.com/todomvc-app-css@2.4.1/index.css";
</style>