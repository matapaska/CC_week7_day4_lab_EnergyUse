<template lang="html">
<div>
 <h1>Energy tracker</h1>
<p>From {{this.dateFrom}} to {{this.dateTo}}</p>
 <energy-sources-list :generationMixForCharts="generationMixForCharts" width = 300px></energy-sources-list>

</div>
</template>

<script>
import EnergySourcesList from './components/EnergySourcesList.vue'
export default {
  data(){
    return{
      energySources: [],
      generationMix: [],
      generationMixForCharts: [["Fuel", "Percentage"]],
      dateFrom: "",
      dateTo: ""

    }
  },
  mounted(){
    fetch('https://api.carbonintensity.org.uk/generation')
    .then(res => res.json())
    .then (data => this.energySources = data)
    .then (() => this.generationMix = this.energySources.data.generationmix)
    .then(() => this.dateFrom = this.energySources.data.from)
    .then(() => this.dateTo = this.energySources.data.to)
    .then(() => this.formatChartData())

  },
  components:{
    "energy-sources-list": EnergySourcesList
  },

  methods:{
    formatChartData: function () {
      const fuel_pair = this.generationMix.forEach((object) => {
          this.generationMixForCharts.push(Object.values(object))
        }
      )
    }

  }

}
</script>

<style lang="css" scoped>
</style>
