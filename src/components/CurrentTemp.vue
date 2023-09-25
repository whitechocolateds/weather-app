<template>
  <div class="card">
    <img :src="imageSrc" />
    <h2>{{ feelsLike }} °C</h2>
    <h3>{{ place }}</h3>
    <section class="moreCondition">
      <p>Conditions: <v-icon icon="mdi-emoticon"></v-icon> {{ currentCond }}</p>
      <p>Humidity<v-icon icon="mdi-water-percent"></v-icon>: {{ humidity }}%</p>
    </section>
    <!--comment-->
  </div>
</template>

<script>
export default {
  props: ['place', 'currentCond', 'icon', 'feelsLike', 'humidity', 'imageSrc'],
};
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  width: 50%;
  height: 90%;
  align-items: center;
  background-image: linear-gradient(90deg, rgba(95, 75, 196, 1) 37%);
  background-size: cover;
  border-radius: 5%;
  border: 2px solid rgb(242, 251, 251);
}
.card img {
  margin-top: 5rem;
  width: 150px;
  height: 150px;
  margin-bottom: 2rem;
}
.card h2 {
  font-size: xx-large;
  margin-bottom: 2rem;
  color: white;
}
.card h1 {
  margin-bottom: 8rem;
  text-align: center;
  color: white;
}
.card h3 {
  color: white;
  text-transform: uppercase;
  text-align: center;
}

.moreCondition {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  margin-top: 7rem;
  color: white;
}
.card h1 {
  margin: 3rem;
  color: white;
}
@media only screen and (max-width: 600px) {
  .card {
    width: 100%;
  }
  .moreCondition {
    margin-bottom: 2rem;
  }
}
</style>
