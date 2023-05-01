<template>
    <div class="detail-produk">
        <NavbarComp />
        <div class="container">
            <nav aria-label="breadcrumb">
                <ol class="breadcrumb mt-4 mb-4">
                    <li class="breadcrumb-item">
                        <router-link to="/" class="text-dark">Home</router-link>
                    </li>
                    <li class="breadcrumb-item">
                        <router-link to="/foods" class="text-dark">Foods</router-link>
                    </li>
                    <li class="breadcrumb-item active" aria-current="page">{{ food.nama }}</li>
                </ol>
            </nav>
            <div class="row">
                <div class="col-md-6">
                    <img :src="'assets/images/' + food.gambar" class="img-fluid rounded shadow" height="220px" alt="...">
                </div>
                <div class="col-md-6">
                    <h2><strong>{{ food.nama }}</strong></h2>
                    <hr>
                    <h4>Harga : <strong>Rp.{{ food.harga }}</strong> </h4>
                    <form v-on:submit.prevent>
                        <div class="form-group mt-4">
                            <label for="jumlah">Jumlah</label>
                            <input type="number" class="form-control" id="jumlah" placeholder="Masukkan jumlah"
                                v-model="pesanan.jumlah_pemesanan">
                        </div>
                        <div class="form-group mt-2">
                            <label for="catatan">Catatan</label>
                            <textarea class="form-control" v-model="pesanan.keterangan" id="catatan" rows="3"
                                placeholder="Masukan Catatan"></textarea>
                        </div>
                        <button type="submit" class="btn btn-success mt-2" @click="kirimPesanan">Pesan
                            <b-icon-cart></b-icon-cart></button>

                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import NavbarComp from "@/components/NavbarComp.vue";
import axios from "axios";


export default {
    name: "FoodDetail",
    components: {
        NavbarComp
    },
    data() {
        return {
            food: {},
            pesanan: {}
        }
    },
    methods: {
        setFood(data) {
            this.food = data;
        },
        kirimPesanan() {
            if(this.pesanan.jumlah_pemesanan){
                this.pesanan.foods = this.food;
            axios
                .post("keranjangs", this.pesanan)
                .then(() => {
                    this.$router.push({ path: "/keranjang"})
                    this.$toast.success('Berhasil Masuk Ke Keranjang', {
                        type: 'success',
                        position: 'top-right',
                        duration: 3000,
                        dismissible: true

                    });
                })
                .catch((error) => {
                    console.log(error);
                });
            } else {
                this.$toast.error('Silahkan Isi Jumlah Pemesanan Terlebih Dahulu', {
                        type: 'error',
                        position: 'bottom-right',
                        duration: 3000,
                        dismissible: true

                    });
            }
        }
    },
    mounted() {
        axios
            .get("products/" + this.$route.params.id)
            .then((response) => {
                this.setFood(response.data);
            })
            .catch((error) => {
                console.log(error);
            });
    }

}
</script>

<style></style>