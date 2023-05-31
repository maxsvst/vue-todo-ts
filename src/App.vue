<template>
  <AppHeader />

  <AppFilters />

  <main class="app-main">
    <AppTodoList
      :todos="todos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <AddAppTodo @add-todo="addTodo" />
  </main>
  <AppFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AddAppTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";
import { Todo } from "./types/todo";

interface State {
  todos: Todo[];
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AddAppTodo,
    AppFooter,
  },
  data(): State {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(todo: Todo) {
      if (todo.text !== "") this.todos.push(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((item: Todo) => item.id === id);
      if (targetTodo) targetTodo.completed = !targetTodo?.completed;
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((item: Todo) => item.id !== id);
    },
  },
});
</script>
