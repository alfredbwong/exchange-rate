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
      <div class="historical-input">
        <span>Historical Data (Against CAD): </span>
        <input type="radio" id="radio-select-usd" name="radio-select" value="USD" v-model="picked" v-on:change="getHistoricalData">
        <label for="USD">USD</label>
        <input type="radio" id="radio-select-gbp" name="radio-select" value="GBP" v-model="picked" v-on:change="getHistoricalData">
        <label for="GBP">GBP</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data : function (){
    return {
      currencies: [
        { name: 'CAD' },
        { name: 'USD' },
        { name: 'GBP' }
      ],
      info: null,
      selectedCurrency: null,
      picked: null
    }
  },
  methods : {
    getRates: function (){
      this.$emit('getRates', this.selectedCurrency)
    },
    getHistoricalData: function(){
      this.$emit('getHistoricalData', this.picked)
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
.historical-input{
  grid-column: 1 / span 2;
}
</style>
