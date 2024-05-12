<script setup>
import { computed, ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

const newtodo = ref()
const todos = ref([])
// const status = ref(false)
function addTodos() {
  if (newtodo.value) {
    todos.value.push({
      id: uuidv4(),
      text: newtodo.value,
      done: false
    })
    newtodo.value = ''
    console.log(todos.value)
  } else {
    alert('Please enter a todo')
  }
}

function removeToDo(id) {
  // console.log(id)
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const todoType = ref('all')

const filteredTodo = computed(() => {
  if (todoType.value === 'active') {
    return todos.value.filter((todo) => !todo.done)
  } else if (todoType.value === 'complete') {
    return todos.value.filter((todo) => todo.done)
  }
  return todos.value
})

function removeCompletedTodos() {
  const findTodosCompleted = todos.value.filter((e) => !e.done)
  // findTodosCompleted.pop()
  todos.value = findTodosCompleted

  // console.log(findTodosCompleted)
}
// const updateStatus = (todo) => {
//   // console.log(status.value)
//   todos.value.find((td) => td.id === todo.id).done = !todo.done
// }

function hasCompleted() {
  return todos.value.filter((e) => e.done).length
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
        <li data-id="4" class="" v-for="todo in filteredTodo" :key="todo">
          <div class="view">
            <input class="toggle" type="checkbox" v-model="todo.done" />

            <label>{{ todo.text }}</label>
            <button class="destroy" @click="removeToDo(todo.id)"></button>
          </div>
        </li>
      </ul>
    </main>
    <footer class="footer" style="display: block">
      <span class="todo-count"
        ><strong> {{ todos.length }} </strong> items left</span
      >
      <ul class="filters">
        <li><a href="#/" class="selected" @click.prevent="todoType = 'all'">All</a></li>
        <li><a href="#/active" class="" @click.prevent="todoType = 'active'">Active</a></li>
        <li><a href="#/completed" @click.prevent="todoType = 'complete'">Completed</a></li>
      </ul>
      <button
        class="clear-completed"
        v-if="hasCompleted()"
        @click="removeCompletedTodos()"
        style="display: block"
      >
        Clear completed
      </button>
    </footer>
  </section>
</template>

<style scoped></style>
