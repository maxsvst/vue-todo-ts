<template>
  <AppHeader />

  <AppFilters :active-filter="activeFilter" @set-filter="setFilter" />

  <main class="app-main">
    <AppTodoList
      :todos="filteredTodos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <AddAppTodo @add-todo="addTodo" />
  </main>
  <AppFooter :stats="stats" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AddAppTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";
import { Filter } from "./types/Filter";
import { Todo } from "./types/Todo";
import { Stats } from "./types/Stats";

interface State {
  todos: Todo[];
  activeFilter: Filter;
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
      activeFilter: "Все",
    };
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case "Активные":
          return this.activeTodos;
        case "Выполненные":
          return this.doneTodos;
        case "Все":
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      };
    },
    activeTodos(): Todo[] {
      return this.todos.filter((item) => !item.completed);
    },
    doneTodos(): Todo[] {
      return this.todos.filter((item) => item.completed);
    },
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
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    },
  },
});
</script>
