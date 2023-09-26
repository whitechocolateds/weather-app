<template>
  <transition name="fade" mode="out-in">
  <div class="app" :key="place">
    <div class="container">
<div class="heading">
  <h1>Weather app</h1>
  <v-text-field
        class="searchBar"
        w-50
        density="compact"
        variant="solo"
        label="Enter location"
        prepend-inner-icon="mdi-magnify"
        single-line
        hide-details         
        v-model="city" 
        @keypress.enter="getWeather"         
      ></v-text-field>
</div>
<div class="main">
  <current-temp 
  :place="place" 
  :currentCond="currentCond"
  :feelsLike="feelsLike"
  :humidity="humidity"
  :icon="icon"
  :imageSrc="imageSrc"
  
  ></current-temp>
  <h2>Daily Forecast</h2>
  <daily-temp :days="days"></daily-temp>  
  
</div>

  </div>
  </div>
  </transition>
</template>

<script>
import axios from 'axios'
import CurrentTemp from './components/CurrentTemp.vue'
import DailyTemp from './components/DailyTemp.vue'

export default {
  name: 'App',
  components: {
    CurrentTemp,
    DailyTemp
  },
  data() {
    return {
      city: '',      
      API_key: 'GZD47XKNVYNRAVV2P9PVE5GGZ',
      place: '',
      currentCond: '',
      feelsLike: '',
      humidity: '',
      icon: '',
      days: '',
      imageSrc: '', 
    }
  },
  created() {
    this.city = 'New York'
    this.getWeather()
    
    
  },
  
  
  methods: {
    getWeather() {
      axios(`https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${this.city}?key=GZD47XKNVYNRAVV2P9PVE5GGZ`).then(data => this.parseData(data)     
        
      ).catch(error => {
    if (error.response && error.response.status === 400) {      
      alert("Place can not be find, try again");
    } else {     
      console.error('An error occurred:', error.message);
    }
    
  })
    },
    parseData(data) {
      
      this.place = data.data.resolvedAddress
      this.currentCond = data.data.currentConditions.conditions
      this.feelsLike = this.getCelzius(data.data.currentConditions.feelslike)
      this.humidity = Math.round(data.data.currentConditions.humidity)
      this.icon = data.data.currentConditions.icon
      this.days = data.data.days
      this.imageSrc = require(`@/assets/${this.icon}.png`)
      
      
    },
    getCelzius(para) {
      const celzius = Math.round((para - 32) * 5 / 9)
       return celzius
    }
    
    
  } 
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Arimo:wght@500&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Arimo', sans-serif;
}
.app{
    width: 100%;
    height: 100%;
    background-image: linear-gradient(to bottom right, rgba(2,0,36,1) 0%, rgba(90,90,186,1) 44%, rgba(0,212,255,1) 100%);
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    
}
.container{
  width: 95%;
  height: 95%;
  background-image: rgba(242,251,251,0.5);  
  border-radius: 97% 3% 98% 2% / 1% 97% 3% 99%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.searchBar{
  flex: 0 0 250px;
  margin-left: 20px;
}

.heading{
  width: 100%;
  height: 5rem;
  display: flex;
  align-items: center;
  justify-content: center; 
}
.heading h1{ 
  text-transform: uppercase;
  color: white;
}
.main{
  display: flex;
  width: 95%;
  height: 90%;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  margin-left: 11rem;
  
  
}
.main h2{
  color: white;
  display: none;
}
@media only screen and (max-width: 600px){
  .app{
    height: 95rem;
  }
  .container{
    align-items: center;
    height: 100%;
  }
  .heading{
    margin-top: 4rem;
  }
 .heading h1{
  display: none;
 }
  .main{
    flex-direction: column;
    margin-top: 3rem;
    width: 90%;
    height: 100%;
  
}
.main h2{
  color: white;
  display: block;
  margin: 2rem 0
}

}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
</style>
