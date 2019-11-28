<template lang="html">
<div>
 <h1>Energy tracker</h1>
<p>From {{this.dateFrom}} to {{this.dateTo}}</p>
 <energy-sources-list :generationMixForCharts="generationMixForCharts" width = 300px></energy-sources-list>
 <date-form></date-form>

</div>
</template>

<script>
import {eventBus} from './main.js'
import EnergySourcesList from './components/EnergySourcesList.vue'
import DateForm from './components/DateForm.vue'
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

    eventBus.$on('date-submit', (startTime, endTime ) => {
      // console.log(formData);
      fetch(`https://api.carbonintensity.org.uk/intensity/stats/${startTime}/${endTime}`)
        .then(res => res.json())
        .then(data => console.log(data))
    } )


  },
  components:{
    "energy-sources-list": EnergySourcesList,
    "date-form": DateForm
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
