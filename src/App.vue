<template>
  <div class="fluid-container bg-dark">
    <div class="container p-5 text-center">
      <h1 class="text-center text-light pb-5">Dog API</h1>
      <img
        :src="dogImg[counter]"
        alt="dog"
        class="img-fluid rounded d-block mx-auto dogImg"
      />
      <Loading class="loading" v-show="loading" />
      <p class="loading text-light" v-show="loading">Loading...</p>
      <button v-on:click="cambiarPerrito" class="btn btn-light btn-lg m-5">
        Ver más perritos
      </button>
      <p class="text-light">Has visto {{ counter }} perritos</p>
    </div>
  </div>

  <footer class="fluid-container bg-dark p-5">
    <p class="text-light text-center">
      Powered by
      <a href="https://daviiduhh.com" class="daviiduhh">daviiduhh</a>
    </p>
  </footer>
</template>

<script>
import Loading from "./components/Loading.vue";

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
    cambiarPerrito: function() {
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

<style>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.dogImg {
  max-width: 80%;
  max-height: 80vh;
}

.daviiduhh {
  text-decoration: none;
  color: white;
}

.daviiduhh:hover {
  color: aquamarine;
}

.loading {
  margin: 0 auto;
  padding: 20px;
}
</style>
