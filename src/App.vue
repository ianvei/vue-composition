<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label for="">New Todo</label>
    <input v-model="data.newTodo" type="text" >
    <div v-for="todo in data.todos" :key="todo.id" :class="{done: todo.done, 'form-entry': 'form-entry'}">
      <h4  @click="toggleDone(todo)">{{todo.content}}</h4>
      <button @click.prevent="deleteTodo(todo)">Delete</button>
      <!-- <input type="checkbox"> -->
    </div>
    <!-- <h3>{{newTodo}}</h3> -->
    <button>Add new todo</button>
    <button @click.prevent="markAllDone">mark all done</button>
  </form>
</template>

<script setup>
import { toValidAssetId } from '@vue/compiler-core';
import { ref, reactive } from 'vue';
 const data = reactive({
  newTodo: '',
  todos: []
 })

 const addNewTodo = () => {
  console.log(data.newTodo);
  data.todos.push({
    id: Date.now(),
    done: false,
    content: data.newTodo
  });
  data.newTodo = '';
  console.log(data.todos);
 }

 const deleteTodo = (individualTodo) => {
  data.todos = data.todos.filter((todo) => todo.id !== individualTodo.id);
 }

  const toggleDone = (individualTodo) => {
    individualTodo.done = !individualTodo.done;
    console.log(data.todos);
  }

  const markAllDone = () => {
    data.todos.forEach((todo) => todo.done = true);
  }

</script>

<style scoped>

body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 80%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;

}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}

.form-entry {
  display: inline-flex;
  align-items: center;
  gap: 20px;
}

.done {
  text-decoration: line-through;
}



</style>
