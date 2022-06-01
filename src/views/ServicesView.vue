<template>
  <ServicesComp></ServicesComp>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ServicesComp from "@/components/Services/ServicesComp.vue";

export default defineComponent({
  name: "ServicesView",
  components: { ServicesComp },
});
</script>
