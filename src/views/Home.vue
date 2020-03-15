<template>
  <div class="home my-12 w-1/3 mx-auto">
    <h1 class="text-4xl mb-8">TODO vue-composition</h1>
    <div
      v-for="todo in state.todos"
      :key="todo.id"
      class="shadow p-4 mb-5 cursor-pointer hover:shadow-lg font-medium relative"
      :class="todo.isComplete && 'bg-light line-through'"
      @click="toggleComplete(todo.id)"
    >
      {{ todo.name }}
      <span
        v-if="todo.isComplete"
        class="text-green  absolute bottom-0 left-0 p-1 text-xs"
      >
        complete
      </span>
    </div>
  </div>
</template>

<script>
import { reactive } from "@vue/composition-api";
import generateArray from "provoke-array";

export default {
  setup() {
    const state = reactive({
      todos: generateArray(10, i => ({
        id: i,
        name: `Todo #${i + 1}`,
        isComplete: false
      }))
    });

    const toggleComplete = id => {
      const newTodos = state.todos.map(item =>
        item.id === id
          ? {
              ...item,
              isComplete: !item.isComplete
            }
          : item
      );
      state.todos = newTodos;
    };

    return { state, toggleComplete };
  }
};
</script>
