<template>
  <div id="todoAdd">
    <v-container>
      <v-row>
        <v-col cols="10">
          <v-text-field
            v-model="taskTextField"
            name="name"
            label="Task"
            id="id"
            @keyup.enter="addTask"
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-btn block elevation="2" color="success" @click="addTask"
            >Add</v-btn
          >
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
// import uuid from "uuid"
import { v4 as uuid } from "uuid";

export default {
  name: "todoAdd",
  methods: {
    addTask() {
      let task = {
        id: uuid(),
        title: this.taskTextField,
        completed: false,
      };
      console.log(task);
      this.$emit("onSubmit", task);
      this.taskTextField = "";
    },
  },
  data() {
    return {
      taskTextField: "",
    };
  },
};
</script>

<style></style>
