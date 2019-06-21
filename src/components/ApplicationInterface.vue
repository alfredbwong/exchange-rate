<template>
  <div id="interface">
    <ControlPanel v-on:getRates="updateExchangeRates"/>
    <TimeSeriesGraph class="item2" v-bind:historicalData="historicalData" />
    <InfoPanel v-bind:info="info"/>
  </div>
</template>

<script>
const axios = require('axios');

import ControlPanel from './interface/ControlPanel.vue'
import InfoPanel from './interface/InfoPanel.vue'
import TimeSeriesGraph from './interface/view/TimeSeriesGraph.vue'
export default {
  
   data : function (){
    return {
      historicalData: null,
      info: null,
      currencyValueSelected: null
    }
  },
  name: 'interface',
  components: {
    ControlPanel,
    InfoPanel,
    TimeSeriesGraph
  },
   methods: {

    updateExchangeRates :function (currencyValueSelected){

      this.currencyValueSelected = currencyValueSelected;
      const vm = this;
      axios.all([
        this.getCurrentRates(),
        this.getHistorialData()
      ])
      .then(axios.spread(function(rateData, historicalData){
        vm.info = rateData.data.rates,
        vm.historicalData = historicalData.data.rates
      }))
    },
    getCurrentRates() {
      return axios.get('https://api.exchangeratesapi.io/latest?base=' + this.currencyValueSelected)
    },
    getHistorialData() {
      var url = 'https://api.exchangeratesapi.io/history?start_at='+this.getPastMonthDate()+'&end_at='+this.getCurrentDate()+'&base=CAD&symbols=USD'
      console.log(url)
      return axios.get(url)
    },
    getCurrentDate(){
      console.log("here")
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth()+1; //As January is 0.
      var yyyy = today.getFullYear();

      if(dd<10) dd='0'+dd;
      if(mm<10) mm='0'+mm;
      return (yyyy+'-'+mm+'-'+dd);
    },
    getPastMonthDate(){
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth();
      var yyyy = today.getFullYear();

      if(dd<10) dd='0'+dd;
      if(mm<10) mm='0'+mm;
      return (yyyy+'-'+mm+'-'+dd);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#interface{
  border: 1px solid;
  display:grid;
  grid-template-columns: 25% auto;
  grid-template-rows: 100px 700px;
  grid-gap: 20px;
}
.item2{
  grid-row: 1 / span 2;
  grid-column: 2;
}
</style>
