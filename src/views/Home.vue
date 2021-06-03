<template>
  <div id="home">
    <h1>Home</h1>
    <v-container>
      <!-- Todo List -->
      <TodoAdd @onSubmit="addTask" />
      <TodoList :todos="todos | reversed" @onDel="delTask" />
      <!-- Todo card -->
      <v-row class="d-flex flex-row justify-content-center align-center">
        <v-img
          contain
          class="mt-10"
          max-height="200"
          src="@/assets/logo.png"
        ></v-img>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoAdd from "@/components/TodoAdd.vue";
import axios from "axios";
export default {
  name: "Home",
  computed: {
    reverseTodo() {
      return this.todos.slice().reverse();
    },
  },
  async mounted() {
    let result = await axios.get("https://jsonplaceholder.typicode.com/todos");
    this.todos = result.data;
  },
  filters: {
    reversed(value) {
      return value.slice().reverse();
    },
  },
  components: {
    TodoList,
    TodoAdd,
  },
  methods: {
    async addTask(task) {
      let result = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        task
      );
      alert(JSON.stringify(result.data));
      this.todos.push(result.data);
      this.taskTextField = "";
    },
    async delTask(id) {
      console.log("item : " + id);
      // this.todos.splice(index, 1); // my own way
      axios
        .delete("https://jsonplaceholder.typicode.com/todos/" + id)
        .then((result) => {
          this.todos = this.todos.filter((item) => item.id !== id);
          console.log(JSON.stringify(result.data));
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  data() {
    return {
      taskTextField: "",
      todos: [],
      todos_mockup: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: false },
        { id: 3, title: "Task 3", completed: false },
        { id: 4, title: "Task 4", completed: true },
      ],
    };
  },
};
</script>
