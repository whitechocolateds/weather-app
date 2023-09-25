<template>
  <div class="card">
    <ul v-for="day in days.slice(1,6)" :key="day.datetime">
    <li>
      <div class="dailyCard">
        <h3>{{  getDayOfWeek(day.datetime)  }}</h3>
        <img :src="require(`@/assets/${day.icon}.png`)">
        <section >
          <h3>{{ getCelzius(day.tempmax)}}°C</h3>
          <h3>{{ getCelzius(day.tempmin) }}°C </h3>          
        </section>
        
      </div>
    </li>
  </ul>
  </div>
</template>

<script>


export default {
  props: ['days'],
  methods: {
    getCelzius(para) {
      const celzius = Math.round((para - 32) * 5 / 9)
       return celzius
    },
    getDayOfWeek(dateString) {
      const date = new Date(dateString);
      const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
      const dayOfWeek = date.getDay();
      const dayName = dayNames[dayOfWeek];
      return dayName;
    }
  },
  computed: {
    
  }
  

}
</script>

<style scoped>
.card{
  display: flex;
  flex-direction: column;
  width: 30%;
  height: 93%;
  
}
.card ul{
  list-style: none;
  display: flex;
  flex-direction: column;
}
.card ul li{
  list-style: none;
}
.dailyCard{
  
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 11rem;
  height: 7rem;
  margin: 2px;
  color: white;
  background-image: linear-gradient(to bottom right, rgba(2,0,36,1) 0%, rgba(90,90,186,1) 44%, rgba(0,212,255,1) 100%);
  background-size: cover;
  border-radius: 5%;
  border: 2px solid rgb(242,251,251);
  
}
.dailyCard img{
  max-width: 3rem;
  max-height: 3rem;
  color: white;
}
.dailyCard section{
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  width: 100%;
  color: white;

}
@media only screen and (max-width: 600px){
  .card{
    display: flex;
    align-items: center;
  }
  .dailyCard{
    width: 14rem;
    margin: 0.5rem;
  }
}
</style>