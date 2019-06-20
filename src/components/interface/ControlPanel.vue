<template>
  <div class="control-panel">
    <h2>Controls</h2>
    <div class="controls">
      <div>Base Currency:</div>
      <div>
        <select v-model="selectedCurrency" v-on:change="getRates" id="baseCurrencySel">
          <option v-for="currency in currencies">
            {{ currency.name }}
          </option>
        </select>
      </div>
      <ul>
        <li v-for="(rate, foreignCurrency) in info">
          {{ rate }} = {{ foreignCurrency}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
const axios = require('axios');

export default {
  data : function (){
    return {
      currencies: [
        { name: 'CAD' },
        { name: 'USD' },
        { name: 'GBP' }
      ],
      info: null,
      selectedCurrency: null
    }
  },
  methods: {

    getRates: function (){
          const vm = this;
          axios.all([
            this.getCurrentRates(), 
          ])
          .then(axios.spread(function(rateData){
            vm.info = rateData.data.rates
          }))
    },
    getCurrentRates() {
      return axios.get('https://api.exchangeratesapi.io/latest?base=' + this.selectedCurrency)
    }
  }
}
  
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.controls{
  display: grid;
  grid-template-columns: 70% auto;
  grid-gap: 5px;
}
.controls select{
  width: 100%;
}
</style>
