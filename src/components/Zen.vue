<template>
    <img :src="dogImg[counter]" alt="dog" class="img-fluid rounded d-block mx-auto dogImg" />
    <Loading class="loading" v-show="loading" />
    <p class="loading text-light" v-show="loading">Loading...</p>
    <button v-on:click="cambiarPerrito" class="btn btn-light btn-lg m-5">
        Ver más perritos
    </button>
    <p class="text-light">Has visto {{ counter }} perritos</p>
</template>

<script>
import Loading from "./Loading.vue";

export default {
    name: "App",
    data() {
        return {
            dogImg: [],
            counter: 1,
            loading: false,
        };
    },
    components: {
        Loading,
    },
    methods: {
        requestData: function () {
            this.loading = true;
            const request = fetch("https://dog.ceo/api/breeds/image/random/50");
            request
                .then((response) => {
                    this.loading = false;
                    return response.json();
                })
                .then((data) => {
                    const imgs = this.dogImg.concat(data.message);
                    this.dogImg = imgs;
                });

            console.log(request);
        },
        cambiarPerrito: function () {
            this.counter++;
            if (this.counter === 50) {
                this.requestData();
            }
        }
    },
    mounted() {
        this.requestData();
    },
};
</script>