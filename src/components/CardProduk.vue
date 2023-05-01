<template>
  <div class="card shadow">
    <img :src=" 'assets/images/' + food.gambar" class="card-img-top" height="220px"  alt="...">
    <div class="card-body">
      <h5 class="card-title">{{ food.nama }}</h5>
      <p class="card-text">Harga : Rp.{{ food.harga }}</p>
      <router-link :to="'/foods/' + food.id" class="btn btn-success"><b-icon-cart></b-icon-cart> Pesan</router-link>
    </div>
</div>
</template>

<script>
export default {
name: 'CardProduk',
props: ['food']
}
</script>

<style>

</style>