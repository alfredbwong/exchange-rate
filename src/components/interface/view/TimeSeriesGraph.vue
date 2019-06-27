<template>
  <GChart type="LineChart" :data="this.historicalData" :options="chartOptions"/>
</template>
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>

<script>
import { GChart } from "vue-google-charts";

export default {
  data() {
    return {
      chartOptions: {
        chart: {
          title: 'Historical Data in Past Year Against the CAD',
          subtitle: 'Sales, Expenses, and Profit: 2014-2017'

        }
      }
    };
  },
  components: {
    GChart
  },
  props: ["historicalData"]
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
