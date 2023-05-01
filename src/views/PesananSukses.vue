<template>
    <div class="pesanan-sukses">
        <NavbarComp />

        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img src="../../public/assets/images/sukses.svg" alt="hero" width="20%" class="img-fluid" srcset="" />
                    <h1>Pesanan Sukses</h1>
                    <h2>Pesanan Anda Sedang Kami Proses</h2>
                    <p>Silahkan Tunggu Sebentar</p>
                    <b-button variant="primary" @click="$router.push('/foods')">Pesan Makanan Lagi</b-button>
                </div>
            </div>
        </div>
    </div>
       
       
  
</template>

<script>
import NavbarComp from "@/components/NavbarComp.vue";
export default {
    name: "PesananSukses",
    components: {
        NavbarComp,
    },

}
</script>

<style>

</style>