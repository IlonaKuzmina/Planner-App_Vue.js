<template>
  <button class="btn__services" :class="{ btnClass }">
    <span class="left__side">{{ buttonName }}</span>
    <span class="right__side">{{ currency }}{{ price }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "@/components/Button/ButtonComp.scss";

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
