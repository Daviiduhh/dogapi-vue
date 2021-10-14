<template>
  <div class="fluid-container bg-dark">
    <div class="container p-5 text-center">
      <h1 class="text-center text-light pb-5">Dog API</h1>
      <img :src="dogImg[counter]" alt="dog" class="img-fluid rounded d-block mx-auto dogImg"/>
      <button v-on:click="counter += 1" class="btn btn-light btn-lg m-5">Ver más perritos</button>
      <p class="text-light">Has visto {{ counter }} perritos</p>
    </div>
  </div>

  <footer class="fluid-container bg-dark p-5">
    <p class="text-light text-center">Powered by
      <a href="https://daviiduhh.com" class="daviiduhh">daviiduhh</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      dogImg: [],
      counter: 0
    };
  },
  async mounted() {
    const res = await fetch("https://dog.ceo/api/breeds/image/random/50");
    const data = await res.json();

    this.dogImg = data.message;

    this.counter += 1
  },
};
</script>

<style>
  .dogImg {
    max-width: 100%;
    max-height: 80vh;
  }

  .daviiduhh {
    text-decoration: none;
    color: white;
  }

  .daviiduhh:hover {
    color: aquamarine;
  }
</style>
