<template>
  <section class="vh-100" style="background-color: #e2d5de;">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center">
        <div class="col col-xl-5">
          <div class="card" style="border-radius: 15px;">
            <div class="card-body p-5">
              <h2 class="mb-3">Todo List</h2>
              <todo-item v-for="(todo, index) in todos" :key="index" :todo="todo" @toggleComplete="toggleComplete(index)"
                @deleteTodo="deleteTodo(index)"></todo-item>
              <todo-form @addTodo="addTodo"></todo-form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

</template>

<script>
import TodoItem from './TodoItem.vue'
import TodoForm from './TodoForm.vue'

export default {
  components: {
    TodoItem,
    TodoForm,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleComplete(index) {
      this.$emit('toggleComplete', index)
    },
    deleteTodo(index) {
      this.$emit('deleteTodo', index)
    },
    addTodo(newTodo) {
      this.$emit('addTodo', newTodo)
    },
  },
}
</script>

<style scoped>
body {
  margin: 0;
  display: grid;
  place-items: center;
  min-height: 100vh;
  background-color: #e5e5e5;
  font-family: system-ui, sans-serif;
  font-weight: 400;
  font-size: 14px;
  color: #484848;
}

.checkbox-container {
  padding: 18px;
  border: 1px solid #e5e5e5;
  background-color: #ffffff;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  width: 250px;
  box-shadow: rgba(149, 157, 165, 0.2) 0 8px 24px;
}

.heading {
  margin-inline: 0;
  margin-block: 6px;
}

.checkbox-group {
  border: 1px solid #e5e5e5;
  padding: 10px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  gap: 6px;
}

.checkbox-group.checked {
  background-color: #0d6efd;
  box-shadow: rgba(13, 110, 253, 0.25) 0 8px 24px;
}

input[type="checkbox"] {
  visibility: hidden;
}

input[type="checkbox"]~label {
  position: relative;
}

input[type="checkbox"]~label:before {
  content: "";
  position: absolute;
  border: 1px solid #e5e5e5;
  height: 14px;
  font-size: 12px;
  aspect-ratio: 1;
  top: 0;
  left: -26px;
  border-radius: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ffffff;
}

input[type="checkbox"]:checked~label {
  color: #ffffff;
}

input[type="checkbox"]:checked~label:before {
  content: "???";
  color: #0d6efd;
}
</style>