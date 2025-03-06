<template>
  <div id="app" class="animate__animated animate__fadeIn">
    <span>
      <h2 class="hour-period">Hora atual: {{ actualHour }}
        - Período: {{ actualPeriod }}
      </h2>
    </span>
    
    <Landscape :actualImage="actualImage"/>
  </div>
</template>

<script>
import Landscape from './components/Landscape/Landscape'
import { format } from 'date-fns'
export default {
  name: 'App',
  components: {
    Landscape
  },

  data(){
    return{
      actualHour: '',
      actualImage: '',
      actualPeriod: 'Manhã'
    }
  },

  methods:{
    theActualHourAndPeriod(){
      let time = new Date();
      let hour = time.getHours()
      const morning = hour >= 5 && hour < 13
      const afternoon = hour >= 12 && hour < 18

      if(morning){
        this.actualImage = require('./assets/dia.jpg')
        this.actualPeriod = 'Manhã'
        document.body.style.backgroundColor = 'lightblue'
      } else if(afternoon){
        this.actualImage = require('./assets/tarde.jpg')
        this.actualPeriod = 'Tarde'
        document.body.style.backgroundColor = 'orange'
      } else {
        this.actualImage = require('./assets/noite.jpg')
        this.actualPeriod = 'Noite'
        document.body.style.backgroundColor = 'black'
      }
    },

    reloadHour(){
      setInterval(() => {
        let time = new Date()
        this.actualHour = `${format(time, 'HH:mm:ss')}`
        document.title = `${format(time, 'HH:mm:ss')} - Hora atual`
      }, 1000);
    }
  },

  mounted(){
    this.reloadHour()
    this.theActualHourAndPeriod()
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 80px;
}

.hour-period{
  text-align: center;
  color: white;
  text-shadow: 2px 2px 2px black;
  font-family: sans-serif;
}
</style>
