<template>
    <h2 class="text-light">Pro</h2>
    <img :src="dogImgs[counter]" alt="Dog img" class="img-fluid rounded d-block mx-auto dogImg" />
    <Loading class="loading" v-show="loading" />
    <p class="loading text-light" v-show="loading">Loading...</p>
    <div>
        <button v-on:click="$emit('anteriorPerrito')" class="btn btn-light btn-lg m-5">
            Anterior
        </button>
        <button v-on:click="$emit('siguientePerrito')" class="btn btn-light btn-lg m-5">
            Siguiente
        </button>
    </div>
    <p class="text-light">Has visto {{ counter }} perritos</p>
</template>

<script>
import Loading from "./Loading.vue";

export default {
    name: "Pro mode",
    data() {
        return {

        };
    },
    props: {
        dogImgs: Array,
        counter: Number,
        loading: Boolean,
    },
    components: {
        Loading,
    }
};
</script>