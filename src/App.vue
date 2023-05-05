<template>
  <link rel="icon" href="/src/assets/logo.png">
  <div id="app">
    <NavBar />
    <router-view />

  </div>
  <div>
    <Footer_custom></Footer_custom>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import Footer_custom from "./components/Footer_custom.vue";
export default {
  name: 'App',
  components: {
    NavBar,
    Footer_custom,
  },
  mounted() {
    document.title = "Turtle-K";
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  font-family: Arial;
}

#page-wrap {
  margin: auto;
  max-width: 900px;
  min-height: 100vh;
}


button {
  background-color: orangered;
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  outline: 0;
  padding: 16px;
}
</style>
