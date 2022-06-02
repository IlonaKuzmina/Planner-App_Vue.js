<template>
  <div class="planner__container">
    <div>
      <div>
        <form @submit.prevent class="input__container">
          <input
            v-model="newTodo"
            class="input"
            type="text"
            placeholder="What is your plann for today?"
            @keypress.enter="addTodo"
          />
          <ButtonComp buttonName="Add" @click="addTodo"></ButtonComp>
        </form>
      </div>

      <div v-for="(todo, index) in getTasksList()" :key="todo.id">
        <div v-if="!todo.isEditing" class="todo__item">
          <input
            type="checkbox"
            name="checkbox"
            id="checkbox"
            :checked="currentFilter === 'Completed'"
            v-model="todo.isCompleted"
          />
          <div
            @click="completeTodo(todo)"
            class="todo__lable"
            :class="{ completed: todo.isCompleted }"
          >
            {{ todo.title }}
          </div>
          <button class="edit__btn" @click="editTodo(todo)">Edit</button>
          <button class="cancel__btn" @click="removeTodo(index)">X</button>
        </div>

        <div class="todo__item edit--container" v-if="todo.isEditing">
          <input class="todo__edite" v-model="todo.title" type="text" />
          <button class="cancel__btn" @click="saveEditedTodo(todo)">
            Save
          </button>
        </div>
      </div>
    </div>

    <div class="button__container">
      <ButtonComp @click="changeFilter('all')" buttonName="All"></ButtonComp>
      <ButtonComp
        @click="changeFilter('inProgress')"
        buttonName="In rogress"
      ></ButtonComp>
      <ButtonComp
        @click="changeFilter('completed')"
        buttonName="Completed"
      ></ButtonComp>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ButtonComp from "@/components/Button/ButtonComp.vue";
import "@/components/Planner/PlannerComp.scss";

type Todos = {
  id: number;
  title: string;
  isEditing: boolean;
  isCompleted: boolean;
};

export default defineComponent({
  name: "PlannerComp",
  components: { ButtonComp },

  data: () => {
    return {
      newTodo: "",
      currentFilter: "",
      idForTodo: 2,
      todos: [] as Todos[],
    };
  },

  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }

      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        isCompleted: false,
        isEditing: false,
      });

      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.newTodo = "";
      this.idForTodo++;
    },

    // getTasksList() {
    //   this.todos = JSON.parse(localStorage.getItem("todos"));
    // },

    removeTodo(index: number) {
      this.todos.splice(index, 1);
    },

    completeTodo(todo: { isCompleted: boolean }) {
      todo.isCompleted = true;
    },

    editTodo(todo: { isEditing: boolean }) {
      todo.isEditing = true;
    },

    saveEditedTodo(todo: { isEditing: boolean }) {
      todo.isEditing = false;
    },

    changeFilter(newFilter: string) {
      this.currentFilter = newFilter;
    },

    getTasksList() {
      if (this.currentFilter === "completed") {
        return this.ongoingTasks;
      } else if (this.currentFilter === "inProgress") {
        return this.doneTasks;
      }
      return this.todos;
    },
  },

  computed: {
    ongoingTasks() {
      return this.todos.filter(({ isCompleted }) => {
        return isCompleted;
      });
    },

    doneTasks() {
      return this.todos.filter(({ isCompleted }) => {
        return !isCompleted;
      });
    },
  },
});
</script>
