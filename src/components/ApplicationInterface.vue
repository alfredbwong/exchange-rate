<template>
  <div id="interface">
    <ControlPanel v-on:getRates="updateExchangeRates"/>
    <div class="item2">Something</div>
    <InfoPanel v-bind:info="info"/>
  </div>
</template>

<script>
const axios = require('axios');

import ControlPanel from './interface/ControlPanel.vue'
import InfoPanel from './interface/InfoPanel.vue'
export default {
  
   data : function (){
    return {
      info: null,
      currencyValueSelected: null
    }
  },
  name: 'interface',
  components: {
    ControlPanel,
    InfoPanel
  },
   methods: {

    updateExchangeRates :function (currencyValueSelected){

      this.currencyValueSelected = currencyValueSelected;
      const vm = this;
      axios.all([
        this.getCurrentRates(), 
      ])
      .then(axios.spread(function(rateData){
        vm.info = rateData.data.rates
      }))
    },
    getCurrentRates() {
      return axios.get('https://api.exchangeratesapi.io/latest?base=' + this.currencyValueSelected)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#interface{
  border: 1px solid;
  display:grid;
  grid-template-columns: 30% auto;
  grid-gap: 20px;
}
.item2{
  grid-row: 1 / span 2;
  grid-column: 2;
}
</style>
