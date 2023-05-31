<template>
  <section class="add-todo">
    <button
      v-show="!isFormVisible"
      class="add-todo__show-form-button"
      @click="toggleFormVisible"
    >
      <i class="bi bi-plus-lg"></i>
    </button>
    <form
      v-show="isFormVisible"
      class="add-todo__form"
      @submit.prevent="addTodo"
    >
      <button class="close-button" type="button" @click="toggleFormVisible">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled" type="submit">Добавить todo</button>
    </form>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Todo } from "../types/todo";

interface State {
  isFormVisible: boolean;
  todoText: string;
}

export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: "",
    };
  },
  methods: {
    toggleFormVisible() {
      this.isFormVisible = !this.isFormVisible;
    },
    addTodo() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      });
      this.todoText = "";
    },
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
});
</script>
