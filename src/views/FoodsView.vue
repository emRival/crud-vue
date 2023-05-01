<template>
  <div>
    <NavbarComp />
    <div class="container">
      <div class="row mt-4">
        <div class="col-md-6">
          <h2>Semua <strong>Makanan</strong></h2>
        </div>
      </div>

      <div class="input-group mb-4 mt-4">
        <input
          v-model="search"
          type="text"
          class="form-control"
          placeholder="Cari Makanan Kesukaan-Mu"
          aria-label="Cari Makanan Kesukaan-Mu"
          aria-describedby="basic-addon1"
          @keyup="searchFood"
        />
        <span class="input-group-text" id="basic-addon1"
          ><b-icon-search></b-icon-search
        ></span>
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
import CardProduk from "@/components/CardProduk.vue";
import axios from "axios";

export default {
  name: "FoodsView",
  components: {
    NavbarComp,
    CardProduk,
  },
  data() {
    return {
      foods: [],
      search: "",
    };
  },
  methods: {
    setFood(data) {
      this.foods = data;
    },
    searchFood() {
      axios
        .get("products?q=" + this.search)
        .then((response) => {
          this.setFood(response.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    axios
      .get("products")
      .then((response) => {
        this.setFood(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style></style>
