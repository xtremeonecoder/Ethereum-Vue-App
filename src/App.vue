<!-- 
 * Ethereum Vue App
 *
 * @category   Application_Frontend
 * @package    ethereum-vue-app
 * @author     Suman Barua
 * @developer  Suman Barua <sumanbarua576@gmail.com>
 -->

<template>
  <div>
    <EthereumPage />
  </div>
</template>

<script>
import EthereumPage from "./components/EthereumPage.vue";

export default {
  name: "App",
  components: {
    EthereumPage,
  },
};
</script>

<style>
h1 {
  margin-top: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#app > div {
  display: flex;
  margin-top: 5rem;
  justify-content: center;
}
#app > div > div {
  width: 70%;
  padding: 3rem;
  box-shadow: 11px 10px 38px 0 rgb(46 63 99 / 15%);
}
</style>
