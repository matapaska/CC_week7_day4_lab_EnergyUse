<template lang="html">
  <div>
<GChart
type = "PieChart"
:data="chartData"
:options="chartOptions"
/>
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'
export default {
  name: "energy-sources-list",
  props: ['generationMixForCharts'],
  components: {
    GChart
  },
  data () {
    return {
      // Array will be automatically processed with visualization.arrayToDataTable function
      chartData: this.generationMixForCharts,
      chartOptions: {
        chart: {
          title: 'Energy sources',
          // subtitle: 'Sales, Expenses, and Profit: 2014-2017',
        }
      }
    }
  }
}
</script>

<style lang="css" scoped>
</style>
