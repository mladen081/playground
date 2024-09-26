<template>
  <h1 :class="titleClass">Home</h1>
  <div class="test-cont">
    <h2>
      Declarative Rendering, <span :class="titleClass">Attribute Bindings</span>, Event Listeners
    </h2>
    <p>ref(): {{ message }}</p>
    <p>reactive({}): {{ counter.count }}</p>
    <fancy-btn @click="increment">Increment</fancy-btn>
    <fancy-btn @click="reset">Reset</fancy-btn>
  </div>
  <div class="test-cont">
    <h2>Form Bindings (two-way bindings)</h2>
    <label for="text1">Text 1</label>
    <input id="text1" :value="text1" @input="onInput" placeholder="Type here" name="text1" />
    <p>{{ text1 }}</p>
    <label for="text2">Text 2</label>
    <input id="text2" v-model="text2" placeholder="Type here" name="text2" />
    <p>{{ text2 }}</p>
  </div>
  <div class="test-cont" style="position: relative">
    <div class="circle">Vue.js</div>
    <h2>Conditional Rendering</h2>
    <fancy-btn @click="toggle">Toggle</fancy-btn>
    <p v-if="awesome">I'm doing well</p>
    <p v-else>oh no 😢</p>
  </div>
  <div class="test-cont">
    <h2>List Rendering and Computed Property</h2>
    <form @submit.prevent="addTodo">
      <label for="newTodo">New Todo</label>
      <input id="newTodo" name="newTodo" v-model="newTodo" required placeholder="New Todo" />
      <fancy-btn>Add Todo</fancy-btn>
    </form>
    <div class="list-container">
      <ul>
        <fieldset>
          <legend style="display: none">completed todos</legend>
          <li v-for="todo in filteredTodos" :key="todo.id">
            <label :for="todo.text">Completed</label>
            <input :id="todo.text" name="completed" type="checkbox" v-model="todo.done" />
            <span :class="{ done: todo.done }">{{ todo.text }}</span>
            <fancy-btn-x @click="removeTodo(todo)">X</fancy-btn-x>
          </li>
        </fieldset>
      </ul>
    </div>
    <fancy-btn @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </fancy-btn>
  </div>
  <div class="test-cont">
    <h2>Lifecycle and Template Refs</h2>
    <p ref="pElementRef">hello</p>
  </div>
  <div class="test-cont" style="height: 400px">
    <h2>Watchers</h2>
    <p>Todo id: {{ todoId }}</p>
    <fancy-btn @click="todoId++" :disabled="!todoData">Fetch Next Todo</fancy-btn>
    <div class="pre-container">
      <p v-if="!todoData">Loading...</p>
      <pre v-else>{{ todoData }}</pre>
    </div>
  </div>
  <div class="test-cont">
    <h2>Components, <span :class="titleClass">Props</span>, Emits</h2>
    <ChildComp :msg="greeting" @response="(msg) => (childMsg = msg)" />
    <p>{{ childMsg }}</p>
  </div>
  <div class="test-cont" style="position: relative">
    <div class="circle">Vue.js</div>
    <h2>Slots</h2>
    <fancy-btn></fancy-btn>
  </div>
</template>

<script setup>
import { reactive, ref, computed, onMounted, watch } from 'vue'

import FancyBtn from '@/components/buttons/FancyBtn.vue'
import FancyBtnX from '@/components/buttons/FancyBtnX.vue'
import ChildComp from '@/components/ChildComponent.vue'

// 1
const message = ref('Hello!')
const titleClass = ref('red')
const counter = reactive({
  count: 0
})
const increment = () => counter.count++
const reset = () => (counter.count = 0)

// 2
const text1 = ref('')
const text2 = ref('')
function onInput(e) {
  text1.value = e.target.value
}

// 3
const awesome = ref(true)
function toggle() {
  awesome.value = !awesome.value
}

// 4
let id = 0
const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Visit S' },
  { id: id++, text: 'Visit M' },
  { id: id++, text: 'Visit A' }
])
const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value
})
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

// 5
const pElementRef = ref(null)
onMounted(() => {
  pElementRef.value.textContent = 'mounted!'
})

// 6
const todoId = ref(1)
const todoData = ref(null)
async function fetchData() {
  todoData.value = null
  const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${todoId.value}`)
  todoData.value = await res.json()
}
fetchData()
watch(todoId, fetchData)

// 7
const greeting = ref('message from parent')
const childMsg = ref('No child msg yet')

// 8
</script>

<style>
.red {
  color: #c21010;
}

.done {
  text-decoration: line-through;
}

.circle {
  color: #c21010;
  position: absolute;
  top: 50%;
  left: 5%;
  display: inline-block;
  width: 100px;
  height: 100px;
  border: 2px solid#c21010;
  border-radius: 50%;
  text-align: center;
  line-height: 5rem;
  font-size: 2rem;
  animation: rotate 20s linear infinite;
}

@keyframes rotate {
  0% {
    transform: translateY(-50%) rotate(0deg); /* Adjusted for rotation */
  }
  100% {
    transform: translateY(-50%) rotate(360deg); /* Complete rotation */
  }
}

@media (max-width: 767px) {
  .circle {
    display: none;
  }
}
</style>
