<template>
  <div id="header-panel">
    <h1>{{  titleText }}</h1>
    <span> Alfred Wong &copy;</span>
    <p> This simple application is for learning purposes. It calls a foreign exchange API and graphs it</p>
  </div>
</template>

<script>
  export default {
    name: 'header-panel',
    data: function() {
      return{
        titleText: 'Exchange Rate Grapher'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div{
  border: solid 1px;
}
</style>
