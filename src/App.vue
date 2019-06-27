<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <HeaderPanel />
    <ApplicationInterface />
  </div>
</template>

<script>

// import HelloWorld from './components/HelloWorld.vue'
import HeaderPanel from './components/HeaderPanel.vue'
import ApplicationInterface from './components/ApplicationInterface.vue'
export default {
  name: 'app',
  components: {
    // HelloWorld,
    HeaderPanel,
    ApplicationInterface
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
