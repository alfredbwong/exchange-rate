<template>
    <li class="rate-list-item">{{ symbol }} : {{ rate }}</li>
       <!-- = {{ foreignCurrency}}</li> -->
</template>

<script>

export default {
  props: ['rate','symbol']
}
  
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.rate-list-item{
  display: inline-block;
  width: 100%;
}
</style>
