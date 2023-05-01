<template>
  <div>
    <b-navbar toggleable="lg" type="light">
  <div class="container">
    <b-navbar-brand href="#">Kulineran</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav class="mr-auto"> <!-- Add mr-auto class here -->
        <li class="nav-item">
          <router-link class="nav-link" to="/">Home</router-link>
        </li>

        <li class="nav-item">
          <router-link class="nav-link" to="/foods">Foods</router-link>
        </li>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <li class="nav-item">
          <router-link class="nav-link" to="/keranjang">
            Keranjang <b-icon-bag></b-icon-bag><span class="badge bg-success ms-2">{{
              updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length
            }}</span>
          </router-link>
        </li>
      </b-navbar-nav>
    </b-collapse>
  </div>
</b-navbar>
  </div>
  <!-- <nav class="navbar navbar-expand-lg bg-body-tertiary bg-light">
    <div class="container">
      <a class="navbar-brand" href="#">Kulineran</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>

          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </ul>

        <ul class="navbar-nav ml-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/keranjang"
              >Keranjang <b-icon-bag></b-icon-bag
              ><span class="badge bg-success ms-2">{{
                updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length
              }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav> -->
</template>

<script>
import axios from "axios";
export default {
  name: "NavbarComp",
  data() {
    return {
      jumlah_pesanan: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    getJumalah(data) {
      this.jumlah_pesanan = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => {
        this.getJumalah(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style></style>