<template>
    <div class="keranjang">
        <NavbarComp :updateKeranjang="keranjangs" />
        <div class="container">
            <nav aria-label="breadcrumb">
                <ol class="breadcrumb mt-3">
                    <li class="breadcrumb-item">
                        <router-link to="/" class="text-dark">Home</router-link>
                    </li>
                    <li class="breadcrumb-item">
                        <router-link to="/foods" class="text-dark">Foods</router-link>
                    </li>
                    <li class="breadcrumb-item active" aria-current="page">Keranjang</li>
                </ol>
            </nav>

            <div class="row">
                <div class="col">
                    <h2>Keranjang <strong>Saya</strong></h2>
                    <div class="table-responsive mt-3">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col">#</th>
                                    <th scope="col">Gambar</th>
                                    <th scope="col">Nama Makanan</th>
                                    <th scope="col">Keterangan</th>
                                    <th scope="col">Jumlah</th>
                                    <th scope="col">Harga</th>
                                    <th scope="col">Total Harga</th>
                                    <th scope="col">Hapus</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(keranjang, index) in keranjangsTerbaru" :key="keranjang.id">
                                    <th>{{ index + 1 }}</th>
                                    <td>
                                        <img :src="'assets/images/' + keranjang.foods.gambar"
                                            class="card-img-top rounded shadow" style="max-width: 300px; max-height: 100px"
                                            alt="gambar" />
                                    </td>
                                    <td>
                                        <strong>{{ keranjang.foods.nama }}</strong>
                                    </td>
                                    <td>
                                        {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                                    </td>
                                    <td>{{ keranjang.jumlah_pemesanan }} Item</td>
                                    <td>Rp. {{ keranjang.foods.harga }}</td>
                                    <td>
                                        Rp. {{ keranjang.foods.harga * keranjang.jumlah_pemesanan }}
                                    </td>
                                    <td align="center">
                                        <b-icon-trash class="text-danger"
                                            @click="hapusKeranjang(keranjang.id)"></b-icon-trash>
                                    </td>
                                </tr>
                                <tr>
                                    <td colspan="6" align="right">
                                        <strong>Total Harga :</strong>
                                    </td>
                                    <td colspan="2">
                                        <strong>Rp. {{ totalHarga }}</strong>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- form checkout -->
            <div class="row justify-content-end">
                <div class="col-md-4">
                    <form v-on:submit.prevent>
                        <div class="form-group mt-4">
                            <label for="nama">Nama Pelanggan :</label>
                            <input type="text" class="form-control" id="nama" placeholder="Tulis Nama Anda"
                                v-model="pesanan.nama">
                        </div>

                        <div class="form-group mt-4">
                            <label for="noMeja">Nomor Meja :</label>
                            <input type="number" class="form-control" id="noMeja" placeholder="Tulis Nomor Meja"
                                v-model="pesanan.noMeja">
                        </div>

                        <button type="submit" class="btn btn-success mt-2 float-end" @click="checkout">Pesan
                            <b-icon-cart></b-icon-cart></button>

                    </form>
                </div>
            </div>
            <!-- end form checkout -->
        </div>
    </div>
</template>

<script>
import NavbarComp from "@/components/NavbarComp.vue";
import axios from "axios";
export default {
    name: "KeranjangView",
    components: {
        NavbarComp,
    },
    data() {
        return {
            keranjangs: [],
            pesanan: {

            },
        };
    },
    methods: {
        setKeranjang(data) {
            this.keranjangs = data;
        },
        hapusKeranjang(id) {
            axios
                .delete("keranjangs/" + id)
                .then(() => {
                    this.$toast.error("Berhasil Menghapus", {
                        type: "error",
                        position: "bottom-right",
                        duration: 3000,
                        dismissible: true,
                    });
                    axios
                        .get("keranjangs")
                        .then((response) => {
                            this.setKeranjang(response.data);
                        })
                        .catch((error) => {
                            console.log(error);
                        });
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        checkout() {
            if (!this.keranjangsTerbaru || this.keranjangsTerbaru.length === 0) {
                this.$toast.error("Keranjang Masih Kosong !", {
                    type: "error",
                    position: "top-right",
                    duration: 3000,
                    dismissible: true,
                });
            } else {
                if (this.pesanan.nama && this.pesanan.noMeja) {
                    this.pesanan.keranjangs = this.keranjangs;
                    axios
                        .post("pesanans", this.pesanan)
                        .then(() => {

                            this.keranjangs.map(function (item) {
                                return axios
                                    .delete("keranjangs/" + item.id)


                                    .catch((error) => {
                                        console.log(error);
                                    });
                            })
                            // refresh keranjang
                            axios
                                .get("keranjangs")
                                .then((response) => {
                                    this.setKeranjang(response.data);
                                })
                                .catch((error) => {
                                    console.log(error);
                                });

                            this.$router.push({ path: "/pesanan-sukses" })
                            this.$toast.success('Sukses Dipesan', {
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
                    this.$toast.error("Harap Isi Nama dan Nomor Meja Terlebih Dahulu", {
                        type: "error",
                        position: "top-right",
                        duration: 3000,
                        dismissible: true,
                    });
                }
            }

        }

    },
    mounted() {
        axios
            .get("keranjangs")
            .then((response) => {
                this.setKeranjang(response.data);
            })
            .catch((error) => {
                console.log(error);
            });
    },
    computed: {
        keranjangsTerbaru() {
            const keranjangsCopy = [...this.keranjangs];
            return keranjangsCopy.sort((a, b) => b.id - a.id);
        },
        totalHarga() {
            return this.keranjangs.reduce(function (items, data) {
                return items + data.foods.harga * data.jumlah_pemesanan;
            }, 0);
        },
    },
};
</script>

<style></style>
