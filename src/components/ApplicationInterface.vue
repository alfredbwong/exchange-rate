<template>
  <div id="interface">
    <ControlPanel v-on:getRates="updateExchangeRates" v-on:getHistoricalData="updateGraph"/>
    <TimeSeriesGraph class="item2" v-bind:historicalData="historicalData"/>
    <InfoPanel v-bind:info="info"/>
  </div>
</template>

<script>
const axios = require("axios");

import ControlPanel from "./interface/ControlPanel.vue";
import InfoPanel from "./interface/InfoPanel.vue";
import TimeSeriesGraph from "./interface/view/TimeSeriesGraph.vue";
export default {
  data: function() {
    return {
      historicalData: null,
      info: null,
      currencyValueSelected: null,
      historicalCurrencyValueSelected: null
    };
  },
  name: "interface",
  components: {
    ControlPanel,
    InfoPanel,
    TimeSeriesGraph
  },
  methods: {
    updateGraph: function(historicalCurrencyValueSelected) {
      this.historicalCurrencyValueSelected = historicalCurrencyValueSelected;
      const vm = this;
      axios.all([this.getHistorialData()]).then(
        axios.spread(function(historicalData) {
          vm.historicalData = vm.formatHistoricalData(
            historicalData.data.rates,
            vm.historicalCurrencyValueSelected
          );
        })
      );
    },
    updateExchangeRates: function(currencyValueSelected) {
      this.currencyValueSelected = currencyValueSelected;
      const vm = this;
      axios.all([this.getCurrentRates()]).then(
        axios.spread(function(rateData) {
          vm.info = rateData.data.rates;
        })
      );
    },
    getCurrentRates() {
      return axios.get(
        "https://api.exchangeratesapi.io/latest?base=" +
          this.currencyValueSelected
      );
    },
    getHistorialData() {
      var url =
        "https://api.exchangeratesapi.io/history?start_at=" +
        this.getPastYearDate() +
        "&end_at=" +
        this.getCurrentDate() +
        "&base=CAD&symbols=" +
        this.historicalCurrencyValueSelected;
      return axios.get(url);
    },
    getCurrentDate() {
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth() + 1; //As January is 0.
      var yyyy = today.getFullYear();

      if (dd < 10) dd = "0" + dd;
      if (mm < 10) mm = "0" + mm;
      return yyyy + "-" + mm + "-" + dd;
    },
    getPastYearDate() {
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth() + 1;
      var yyyy = today.getFullYear() - 1;

      if (dd < 10) dd = "0" + dd;
      if (mm < 10) mm = "0" + mm;
      return yyyy + "-" + mm + "-" + dd;
    },
    formatHistoricalData(jsonData, currencySymbol) {
      var data = [];

      for (var i in jsonData) {
        data.push([i, jsonData[i][currencySymbol]]);
      }
      var sorteddata = data.sort(function(a, b) {
        var c = new Date(a[0]);
        var d = new Date(b[0]);
        return c - d;
      });
      data.unshift(["Date", "Rate"]);
      return data;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#interface {
  border: 1px solid;
  display: grid;
  grid-template-columns: 25% auto;
  grid-template-rows: 100px 700px;
  grid-gap: 20px;
}
.item2 {
  grid-row: 1 / span 2;
  grid-column: 2;
}
</style>
