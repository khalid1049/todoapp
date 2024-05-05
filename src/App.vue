<script setup>
import { ref } from 'vue'

const newtodo = ref()
const todos = ref([])
function addTodos() {
  if (newtodo.value) {
    todos.value.push({
      text: newtodo.value,
      done: false
    })
    newtodo.value = ''
  } else {
    alert('Please enter a todo')
  }
}
</script>

<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input
        class="new-todo"
        placeholder="What needs to be done?"
        autofocus=""
        v-model="newtodo"
        @keyup.enter="addTodos"
      />
    </header>
    <main class="main" style="display: block">
      <div class="toggle-all-container">
        <input class="toggle-all" type="checkbox" />
        <label class="toggle-all-label" for="toggle-all">Mark all as complete</label>
      </div>
      <ul class="todo-list">
        <li data-id="4" class="" v-for="todo in todos" :key="todo">
          <div class="view">
            <input class="toggle" type="checkbox" />
            <label>{{ todo }}</label>
            <button class="destroy"></button>
          </div>
        </li>
      </ul>
    </main>
    <footer class="footer" style="display: block">
      <span class="todo-count"><strong>2</strong> items left</span>
      <ul class="filters">
        <li><a href="#/" class="selected">All</a></li>
        <li><a href="#/active" class="">Active</a></li>
        <li><a href="#/completed">Completed</a></li>
      </ul>
      <button class="clear-completed" style="display: block">Clear completed</button>
    </footer>
  </section>
</template>

<style scoped></style>
