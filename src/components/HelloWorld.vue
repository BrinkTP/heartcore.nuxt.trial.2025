<script setup lang="ts">
import { reactive, ref, type Ref, computed } from 'vue'
import LifeCycles from './LifeCycles.vue'
import ParentComp from './ParentComp.vue'

class Todo {
  id: number
  text: string
  done: boolean

  constructor(id: number, text: string, done: boolean) {
    this.id = id
    this.text = text
    this.done = done
  }
}
const message = ref('Hello World!')
const subText = ref('')
const titleClass = ref('title')
const counter = reactive({
  count: 0
})

var hideCompleted = ref(false);
const filteredTodos = computed(() => {
  // return filtered todos based on
  // `todos.value` & `hideCompleted.value`
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

var id = 0;
const todos: Ref<Todo[]> = ref([
  new Todo(id++, 'Learn HTML', true),
  new Todo(id++, 'Learn JavaScript', false),
  new Todo(id++, 'Learn Vue', true)
])
const newTodo = ref('')

function changeCounterBy(increment: number) {
  counter.count += increment
}

function addTodo() {
  todos.value.push(new Todo(id++, newTodo.value, true))
  newTodo.value = ''
}

function removeTodo(todo: Todo) {
  const index = todos.value.indexOf(todo)
  if (index > -1) {
    todos.value.splice(index, 1)
  }
}
</script>

<template>
  <div class="flexbox">
    <div>
      <h1 :class="titleClass">{{ message }}</h1>
      <p>SubText is: {{ subText }}</p>
      <input v-model="subText">
    </div>
    <div>
      <p>Count is: {{ counter.count }}</p>

      <button v-if="counter.count < 10" @click="changeCounterBy(1)">Increment!</button>
      <button v-if="counter.count > 0" @click="changeCounterBy(-1)">Decrement!</button>
    </div>
    <div class="pt-2">
      <h2>ToDo list</h2>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="new todo">
        <button type="submit">Add Todo</button>
      </form>
      <button @click="hideCompleted = !hideCompleted">Hide/show</button>
      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <input type="checkbox" v-model="todo.done">
          <span :class="todo.done ? 'strike' : ''">{{ todo.text }}</span>
          <button @click="removeTodo(todo)">Delete</button>
        </li>
      </ul>
    </div>
    <LifeCycles />
    <ParentComp />
  </div>
</template>

<style scoped>
h1 {
  color: #42b983;
  font-size: 2em;
  text-align: center;
}

p {
  color: #42b983;
  font-size: 2em;
  text-align: center;
}

.flexbox {
  display: flex;
  gap: 0.5rem;
  > * {
    border: 1px dashed greenyellow;
    padding: 20px;
  }
}

.title {
  color: red;
}

.strike {
  text-decoration: line-through
}

.pt-2 {
  padding-top: 5em;
}
</style>
