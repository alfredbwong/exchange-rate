<template>
  <div class="info-panel">
    <h2>Exchange Rates</h2>
    <ul class="exchange-rate-list">
      <ExchangeRateInfo
        v-bind:key="symbol"
        v-for="(exchangeRate, symbol) in info" 
        v-bind:rate="exchangeRate"
        v-bind:symbol="symbol"/>
    </ul>
  </div>
</template>

<script>
import ExchangeRateInfo from './view/ExchangeRateInfo.vue'

export default {
  name: 'info-panel',
  components: {
    ExchangeRateInfo
  },
  props: ['info']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.exchange-rate-list{
  list-style-type: none;
  padding:0;
}
</style>
