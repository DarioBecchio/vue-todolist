<script>
export default {
  name: "App",

  data() {
    return {
      newTask: "",
      error: null,
      todoList: [
        {
          text: "Lavare la macchina",
          done: true,
        },
        {
          text: "Dare da bere alle piante",
          done: false,
        },
        {
          text: "Fare trenta minuti di ciclette",
          done: false,
        },
      ],
    };
  },

  methods: {
    removeTask(index) {
      console.log("rimuovi questa task");
      this.todoList.splice(index, 1);
    },

    addTask() {
      if (this.newTask.length > 5) {
        this.todoList.unshift({ text: this.newTask, done: false });
        this.newTask = "";
      } else {
        this.error = "This should be at least long 5 character";
      }
    },
  },

  updated() {
    console.log(this.todoList);
  },
};
</script>

<template>
  <div class="container">
    <h1>Todolist</h1>
    <input type="text" v-model="newTask" @keyup.enter="addTask" />
    <button @click="addTask">Aggiungi task</button>
    <p>{{ error }}</p>
    <ul v-if="todoList.length > 0">
      <li v-for="(element, index) in todoList">
        <span :style="{ textDecoration: element.done ? 'line-through' : '' }">
          {{ element.text }}
        </span>
        <span @click="removeTask()"> X </span>
      </li>
    </ul>
    <p v-else="todoList">Niente da fare</p>
  </div>
</template>

<style></style>
