<template lang="html">
  <form v-on:submit="handleForm">
    <label for="start_date">Select start date</label>
    <input type="datetime-local" id="start_date" v-model="startForm" >
    <br>
    <label for="end_date">Select end date</label>
    <input type="datetime-local" id="end_date" v-model="endForm" >
    <br>
    <input type="submit" value="Enter dates">

  </form>

</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'date-form',
  methods:{
    handleForm(event){
      event.preventDefault();
      eventBus.$emit('date-submit', this.startForm, this.endForm)

    }
  },
  data(){
    return {
    startForm: "",
    endForm: ""
    }
  }
}
</script>

<style lang="css" scoped>
</style>
