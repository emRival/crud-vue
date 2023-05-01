<template>
    <div class="hero">
        <div class="d-none d-md-block">
            <div class="row mt-4">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="align-content-center align-self-center">
                            <h2>
                                <Strong>Delicious Foods Menu, </Strong> <br />
                                in Your Gadget
                            </h2>
                            <p>Ayo Segera Pilih dan Pesan Makanan Favorite-Mu Disini</p>
                            <router-link to="/foods" class="btn btn-success"><b-icon-arrow-right></b-icon-arrow-right> Pesan
                                Sekarang</router-link>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <img src="../../public/assets/images/hero.svg" alt="hero" width="65%" srcset="" />
                </div>
            </div>
        </div>
        <div class="d-sm-block d-md-none">
            <div class="row mt-4 text-center">
                <div class="col-md-6 mb-4">
                    <img src="../../public/assets/images/hero.svg" alt="hero" width="65%" class="img-fluid" srcset="" />
                </div>
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="align-content-center align-self-center">
                            <h2>
                                <Strong>Delicious Foods Menu, </Strong> <br />
                                in Your Gadget
                            </h2>
                            <p>Ayo Segera Pilih dan Pesan Makanan Favorite-Mu Disini</p>
                            <router-link to="/foods" class="btn btn-success"><b-icon-arrow-right></b-icon-arrow-right> Pesan
                                Sekarang</router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "HeroSection",
};
</script>

<style></style>
