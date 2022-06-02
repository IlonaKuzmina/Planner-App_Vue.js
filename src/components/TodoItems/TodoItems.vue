<template>
  <div class="todo__items">
    <div v-if="!isEditing" class="todo__item">
      <input
        type="checkbox"
        name="checkbox"
        id="checkbox"
        v-model="isCompleted"
      />
      <div
        @click="completeTodo"
        class="todo__lable"
        :class="{ completed: isCompleted }"
      >
        {{ todo.title }}
      </div>
      <button class="edit__btn" @click="editTodo">Edit</button>
      <button class="cancel__btn" @click="removeTodo(index)">X</button>
    </div>

    <div class="todo__item edit--container" v-if="isEditing">
      <input class="todo__edite" v-model="title" type="text" />
      <button class="cancel__btn" @click="saveEditedTodo">Save</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "@/components/PlannerInput/TodoItems.scss";

export default defineComponent({
  name: "TodoItems",
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },

  data() {
    return {
      id: this.todo.id,
      title: this.todo.title,
      isCompleted: this.todo.isCompleted,
      isEditing: this.todo.isEditing,
    };
  },

  methods: {
    removeTodo(index: number) {
      this.$emit("removeTodo", index);
    },

    editTodo() {
      this.isEditing = true;
    },

    saveEditedTodo() {
      this.isEditing = false;
    },

    completeTodo() {
      this.isCompleted = true;
    },
  },
});
</script>
