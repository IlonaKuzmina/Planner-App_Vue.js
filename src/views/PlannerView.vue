<template>
  <div>
    <PlannerComp1></PlannerComp1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PlannerComp1 from "@/components/Planner/PlannerComp.vue";

export default defineComponent({
  name: "PlannerView",
  components: {
    PlannerComp1,
  },
});
</script>
