<template>
  <div class="TodoPage">
    <h1 class="text-white">{{ title }}</h1>
    <v-text-field rounded class="InputTodo" type="text" label="Enter to todo" v-model="todo"
                  v-on:keyup.enter="addTodo(id++)"/>
    <div v-for="(todo,idx) in todos" :key="todo.id">
<!--      <div class="ch">-->
        <div class="Todos">
          <v-checkbox class="CheckBox" v-model="todo.isCompleted" color="success" hide-details/>
          <div class="TodoId">{{ idx + 1 }}</div>
          <div class="Todo" :class="{Completed: todo.isCompleted}">{{ todo.text }}</div>
          <span class="DateCheck">{{ date }}</span>
          <v-icon class="DeleteTodo" @click="removeTodo(idx)">mdi-trash-can-outline</v-icon>
        </div>
<!--      </div>-->
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-page",
  data: () => ({
    title: "Мои Задачи",
    todo: "",
    todos: [],
    isCompleted: false,
    id: 0,
    date: ""
  }),
  mounted() {
    const data = localStorage.getItem("todos")
    data ? this.todos = JSON.parse(data) : null
  },
  methods: {
    addTodo() {
      if (this.todo !== "") {
        this.todos.push({
          id: this.id,
          text: this.todo,
          date: this.date,
          isCompleted: this.isCompleted
        })
        this.date = new Date().toLocaleDateString()
        localStorage.setItem("todos", JSON.stringify(this.todos))
      }
      this.todo = ""
    },
    removeTodo(idx) {
      this.todos.splice(idx, 1)
      localStorage.setItem("todos", JSON.stringify(this.todos))
    }
  }
}
</script>

<style scoped lang="sass">
.InputTodo
  color: white
  max-width: 600px
  margin-top: 40px
  margin-right: auto
  margin-left: auto

.Completed
  color: white
  text-decoration: line-through

.Todos
  font-size: 20px
  display: flex
  justify-content: space-evenly
  cursor: pointer
  color: white
  border: 5px solid #4b5563
  border-radius: 40px
  background-color: #374151
  width: 888px
  margin-right: auto
  margin-left: auto
  margin-bottom: 10px

.DateCheck
  color: darkgray
  margin-top: 13px

.CheckBox
  max-width: 45px
  max-height: 45px
  margin-bottom: 10px
.Todo
  margin-top: 13px

.TodoId
  margin-top: 13px

.DeleteTodo
  margin-top: 13px
  &:hover
    color: #ef4444

</style>