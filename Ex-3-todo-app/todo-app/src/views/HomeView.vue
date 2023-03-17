<template>
  <div class="content mx-5">
    <h1>Todo App</h1>
    <form @submit.prevent="addTodo">
      <div class="field">
        <div class="control">
          <input type="text" v-model="todo" class="input" placeholder="Todo Girin">
        </div>
      </div>
      <button type="submit" class="button is-warning">Ekle</button>
    </form>
    <div v-for="todo in todos" :key="todo.id" class="card my-5 mx-5">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content">
            <p class="title cursor" @click="done(todo)" :class="{ done: todo.done }">
              {{todo.content}}
            </p>
            <p>Yapıldı: {{todo.done}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: 'HomeView',
  setup() {
    const todo = ref("");
    const todos = ref([]);

    function addTodo() {
      todos.value.push({
        done: false,
        content: todo.value,
        id: Date.now(),
      });
      todo.value = "";
    }

    function done(todo) {
      todo.done = !todo.done
    }

    return { todo, todos, addTodo, done };
  }
}
</script>

<style>
.cursor {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
