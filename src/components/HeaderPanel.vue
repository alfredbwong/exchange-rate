<template>
  <div id="header-panel">
    <h1>{{  titleText }}</h1>
    <img id="logo" alt="Vue logo" src="../assets/companylogo.png">
    <p> Alfred Wong &copy;</p>
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
#header-panel{
  background-color: #6299be;
}
div{
  border: solid 1px;
}
#logo{
  height: 150px;
  width: 150px;
  margin: auto;
}
</style>
