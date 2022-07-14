<template>
  <header class="header p-3">
    <h1 class="text-center text-light px-3">Dog API</h1>
    <div class="header__mode px-3 d-flex align-items-center">
      <h5 class="text-light m-0">Mode: </h5>
      <button class="btn btn-info text-capitalize mx-3" v-text="mode" @click="changeMode"></button>
    </div>
  </header>
  <main class="fluid-container">
    <div class="container p-3 text-center">
      <Zen v-if="mode == 'zen'" :dogImgs="dogImgs" :counter="sawDogs" :loading="loading"
        @siguientePerrito="siguientePerrito" />
      <Pro v-else :dogImgs="dogImgs" :counter="sawDogs" :loading="loading" @siguientePerrito="siguientePerrito" />
      <p class="text-light">Has visto {{ sawDogs }} perritos</p>
    </div>
  </main>

  <footer class="fluid-container p-5">
    <p class="text-light text-center">
      See this repository
      <a href="https://github.com/Daviiduhh/dogapi-vue" class="daviiduhh">Daviiduhh's GitHub</a>
    </p>
  </footer>
</template>

<script setup>
import { ref, onMounted } from 'vue';

import Zen from './components/Zen.vue'
import Pro from './components/Pro.vue'

onMounted(() => {
  console.log('mounted');
  requestData();
})

const emit = defineEmits(['siguientePerrito', ''])

const mode = ref('zen')
const loading = ref(false)
const dogImgs = ref([])
const sawDogs = ref(1)

function changeMode() {
  const value = mode.value

  if (value == 'zen') {
    mode.value = 'pro'
  } else if (value == 'pro') {
    mode.value = 'zen'
  }
}

function requestData() {
  loading.value = true;
  const request = fetch("https://dog.ceo/api/breeds/image/random/50");
  request
    .then((response) => {
      loading.value = false;
      return response.json();
    })
    .then((data) => {
      dogImgs.value = dogImgs.value.concat(data.message);
    });

  console.log(dogImgs);
}

function siguientePerrito() {
  sawDogs.value++;
  if (sawDogs.value === 50) {
    requestData();
  }
}
</script>

<style>
body {
  background-color: #282c34 !important;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

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

.header {
  display: flex;
  justify-content: space-between;
}

.daviiduhh {
  color: white;
  font-weight: 900;
}

.daviiduhh:hover {
  color: aquamarine;
}

.loading {
  margin: 0 auto;
  padding: 20px;
}
</style>
