<template>
  <div class="services__container">
    <h1 class="title">Services</h1>
    <ButtonServices
      v-for="service in services"
      :key="service.id"
      :buttonName="service.title"
      :price="service.price"
      :currency="service.currency"
      v-model="service.isSelected"
      @click="isSelected(service, price)"
      :class="{ isSelected: service.isSelected }"
    ></ButtonServices>
    <hr class="line" />
    <div class="total__container">
      <span>Total:</span>
      <span>{{ currency }}{{ parseInt(total.toFixed(2)) }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "@/components/Services/ServicesComp.scss";
import ButtonServices from "../Button/ButtonServices.vue";

export default defineComponent({
  name: "ServicesComp",
  components: { ButtonServices },

  data: () => {
    return {
      newTotal: 0,
      total: 0,
      currency: "$",
      services: [
        {
          id: 1,
          title: "Web Development",
          currency: "$",
          price: 300,
          isSelected: false,
        },
        {
          id: 2,
          title: "Designe",
          currency: "$",
          price: 400,
          isSelected: false,
        },
        {
          id: 3,
          title: "Integration",
          currency: "$",
          price: 250,
          isSelected: false,
        },
        {
          id: 4,
          title: "Training",
          currency: "$",
          price: 220,
          isSelected: false,
        },
      ],
    };
  },

  methods: {
    isSelected(service: { isSelected: boolean; price: number }) {
      if (!service.isSelected) {
        service.isSelected = true;
        this.total = this.total + service.price;
      } else {
        service.isSelected = false;
        this.total = this.total - service.price;
      }
    },
  },
});
</script>
