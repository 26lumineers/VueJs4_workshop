<template>
  <div id="todoList">
    <v-card elevation="2">
      <v-card-title primary-title>
        <v-container>
          <v-row
            class="d-flex flex-row align-center"
            v-for="(item, index) in todos"
            :key="index"
          >
            <v-col class="d-flex flex-row align-center pa-0" cols="12">
              <v-checkbox class="mr-2" v-model="item.completed"></v-checkbox>
              <span>{{ item.title }}</span>
              <v-spacer></v-spacer>
              <v-btn small elevation="2" color="error" @click="delTask(item)"
                >X</v-btn
              >
            </v-col>
            <v-col>
              <v-divider></v-divider>
            </v-col>
          </v-row>
        </v-container>
      </v-card-title>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "todoList",
  props: ["todos"],
  methods: {
    delTask(item) {
      this.$emit("onDel", item.id);
    },
  },
};
</script>

<style></style>
