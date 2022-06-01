<template>
  <button class="btn">{{ buttonName }}</button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "@/components/Button/ButtonComp.scss";

export default defineComponent({
  name: "ButtonComp",
  props: {
    buttonName: String,
  },
});
</script>
