<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append-inner="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      append-inner-icon="mdi-plus"
      label="Add Task"
      variant="outlined"
      clearable
      hide-details
    ></v-text-field>
    <v-switch
      :model-value="false"
      @click:prepend="filterComplete(task.id)"
      color="primary"
      label="Completed"
      class="ml-10"
    ></v-switch>

    <div v-for="task in tasks" :key="task.id">
      <v-list lines="three" select-strategy="classic">
        <v-list-item @click="doneTask(task.id)" :class="{ blue: task.done }">
          <template v-slot:prepend="{}">
            <v-list-item-action>
              <v-checkbox-btn v-model="task.done"></v-checkbox-btn>
            </v-list-item-action>
          </template>
          <v-list-item-title>{{ task.title }}</v-list-item-title>
          <template v-slot:append>
            <v-btn color="grey-1" icon="mdi-pencil" variant="text"></v-btn>
            <v-btn
              @click.stop="deleteTask(task.id)"
              color="grey-1"
              icon="mdi-delete"
              variant="text"
            ></v-btn>
          </template>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
import { defineComponent } from "vue";

// Components

export default defineComponent({
  name: "HomeView",
  data() {
    return {
      newTaskTitle: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      let newTask = {
        id: uuidv4(),
        title: this.newTaskTitle,
        done: false,
      };
      console.log(newTask);
      this.tasks.push(newTask);
      this.newTaskTitle = "";
    },
    // filterComplete(id) {
    //   let complete = this.tasks.filter((id) => task.id === task.done);
    //   console.log(complete);
    // },
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
});
</script>
