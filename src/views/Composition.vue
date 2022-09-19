<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h3>You have {{ todosCount }} todos</h3>
    <div>
      <input
        type="text"
        placeholder="enter todo"
        v-model="newTodoName"
        @keyup.enter="addTodo"
      />
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch } from "vue";

export default {
  setup() {
    let newTodoName = ref("");
    let todos = ref([
      {
        id: 1,
        name: "one",
      },
      {
        id: 2,
        name: "two",
      },
      {
        id: 3,
        name: "three",
      },
    ]);
    const swearWords = ["asswipe", "dickhead", "moron"];

    let todosCount = computed(() => {
      return todos.value.length;
    });

    function addTodo() {
      todos.value.push({
        id: Date.now(),
        name: newTodoName.value,
      });
      newTodoName.value = "";
    }

    function deleteTodo(index) {
      todos.value.splice(index, 1);
    }

    watch(newTodoName, (newValue) => {
      if (swearWords.includes(newValue.toLowerCase())) {
        newTodoName.value = "";
        alert(`you must never say ${newValue}!!!`);
      }
    });

    return {
      newTodoName,
      todos,
      addTodo,
      deleteTodo,
      todosCount,
    };
  },
};
</script>