<template lang="html">
<div>
 <h1>Energy tracker</h1>
 <energy-sources-list :energy-sources="energySources" ></energy-sources-list>
</div>
</template>

<script>
import EnergySourcesList from './components/EnergySourcesList.vue'
export default {
  data(){
    return{
      energySources: [],
      generationMix: []

    }
  },
  mounted(){
    fetch('https://api.carbonintensity.org.uk/generation')
    .then(res => res.json())
    .then (data => this.energySources = data)
    .then (() => this.generationMix = this.energySources.data.generationmix)

  },
  components:{
    "energy-sources-list": EnergySourcesList
  }

}
</script>

<style lang="css" scoped>
</style>
