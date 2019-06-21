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
      selectedCurrency: null
    }
  },
  methods : {
    getRates: function (){
      this.$emit('getRates', this.selectedCurrency)
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
