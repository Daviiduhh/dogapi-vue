<template>
    <h2 class="text-light">Pro</h2>
    <img :src="dogImgs[index]" alt="Dog img" class="img-fluid rounded d-block mx-auto dogImg" />
    <Loading class="loading" v-show="loading" />
    <p class="loading text-light" v-show="loading">Loading...</p>
    <div>
        <button v-on:click="decrease" class="btn btn-light btn-lg m-5">
            Anterior
        </button>
        <button v-on:click="increase" class="btn btn-light btn-lg m-5">
            Siguiente
        </button>
        <p class="text-light">Estas viendo el perrito {{ index }} de {{ counter }}</p>
    </div>
</template>

<script>
import Loading from "./Loading.vue";

export default {
    name: "Pro mode",
    data() {
        return {
            index: 1
        };
    },
    methods: {
        increase() {
            if(this.index == this.counter) {
                this.$emit('siguientePerrito');
            }
            this.index++;
        },
        decrease() {
            if (this.index > 1) {
                this.index--;
            }
        }
    },
    mounted() {
        this.index = this.counter
    },
    props: {
        dogImgs: Array,
        counter: Number,
        loading: Boolean,
    },
    components: {
        Loading,
    },
    emits: ['siguientePerrito']
};
</script>