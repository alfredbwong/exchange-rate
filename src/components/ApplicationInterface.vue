<template>
  <div id="interface">
    <ControlPanel />
    <InfoPanel />
  </div>
</template>

<script>
import ControlPanel from './interface/ControlPanel.vue'
import InfoPanel from './interface/InfoPanel.vue'
export default {
  name: 'interface',
  components: {
    ControlPanel,
    InfoPanel
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
</style>
