<template>
        <GChart
            type="LineChart"
            :data="this.historicalData"
        />
</template>
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>

<script>
import { GChart } from 'vue-google-charts'

    export default {
        components: {
            GChart
        },
        props: ['historicalData']
    }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
