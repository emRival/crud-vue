<template>
  <div class="home">
    <NavbarComp />
    <div class="container">
      <HeroSection />

      <div class="row mt-4">
        <div class="col-md-6">
          <h2>Popular <strong>Foods</strong></h2>
        </div>

        <div class="col-md-6 text-end">
          <router-link to="/foods" class="btn btn-success"><b-icon-eye></b-icon-eye> Lihat Semua</router-link>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col-md-4 mb-4" v-for="food in foods" :key="food.id">
          <CardProduk :food="food" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavbarComp from "@/components/NavbarComp.vue";
import HeroSection from "@/components/HeroSection.vue";
import CardProduk from "@/components/CardProduk.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    NavbarComp,
    HeroSection,
    CardProduk,
  },
  data() {
    return {
      foods: [],
    };
  },
  methods: {
    setFood(data) {
      this.foods = data;
    },
  },
  mounted() {
    axios
      .get("best-products")
      .then((response) => {
        this.setFood(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
