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
export default {
  data() {
    return {
      newTodoName: "",
      todos: [
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
      ],
      swearWords: ["asswipe", "dickhead", "moron"],
    };
  },

  computed: {
    todosCount() {
      return this.todos.length;
    },
  },

  methods: {
    addTodo() {
      this.todos.push({
        id: Date.now(),
        name: this.newTodoName,
      });
      this.newTodoName = "";
    },

    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },

  watch: {
    newTodoName(newValue) {
      if (this.swearWords.includes(newValue.toLowerCase())) {
        this.newTodoName = "";
        alert(`You must never say ${newValue}!!!`);
      }
    },
  },
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}

li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}

li span {
  flex-grow: 1;
}
</style>
