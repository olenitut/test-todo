<script>
import TodoItem from './components/ItemTodo.vue'
import TodoForm from './components/FormTodo.vue'

const todos = []

export default {
  name: 'app',

  components: {
    TodoItem,
    TodoForm
  },

  data() {
    return {
      todos
    }
  },

  methods: {
    addTodo(toDotitle) {
      this.todos.push({
        id: Date.now(),
        title: toDotitle,
        done: false
      })
    },

    updateStatus(toDoId) {
      const neededTodo = this.todos.find((item) => item.id === toDoId)
      neededTodo.completed = !neededTodo.completed
    },

    deleteTodo(toDoId) {
      const itemIndex = this.todos.findIndex((item) => item.id === toDoId)
      this.todos.splice(itemIndex, 1)
    },

    editToDo(toDoId, newTask) {
      const neededTodo = this.todos.find((item) => item.id === toDoId)
      neededTodo.title = newTask
    }
  },

  computed: {
    stats() {
      console.log(this.todos)
      const finished = this.todos.filter((item) => item.completed).length
      return `${this.todos.length - finished} tasks left to do, ${finished} completed`
    }
  }
}
</script>

<template>
  <div id="app">
    <h1 class="todo__heading">What do you need to do?</h1>
    <todo-form @todo-added="addTodo"></todo-form>
    <ul class="todo__list">
      <li v-for="item in todos" :key="item.id">
        <todo-item
          :title="item.title"
          :completed="item.completed"
          :id="item.id"
          @status-changed="updateStatus(item.id)"
          @item-deleted="deleteTodo(item.id)"
          @item-edited="editToDo(item.id, $event)"
        >
        </todo-item>
      </li>
    </ul>
    <p class="todo__stats">{{ stats }}</p>
  </div>
</template>
