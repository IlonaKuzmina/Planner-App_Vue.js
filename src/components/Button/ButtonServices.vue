<template>
  <button class="btn__services" :class="{ active: btnClass }">
    <span class="left__side">{{ buttonName }}</span>
    <span class="right__side">{{ currency }}{{ price }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ButtonServices",
  props: {
    buttonName: String,
    currency: String,
    price: String,
    btnClass: String,
  },
});
</script>

<style scoped lang="scss" src="./ButtonComp.scss"></style>
