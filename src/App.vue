<template>
  <main class="fluid-container">
    <div class="container p-5 text-center">
      <h1 class="text-center text-light pb-5">Dog API</h1>
      <Zen />
    </div>
  </main>

  <footer class="fluid-container p-5">
    <p class="text-light text-center">
      Powered by
      <a href="https://daviiduhh.com" class="daviiduhh">daviiduhh</a>
    </p>
  </footer>
</template>

<script setup>
import Zen from './components/Zen.vue'

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
