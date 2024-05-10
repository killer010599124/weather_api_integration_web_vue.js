<script setup>
import {ref} from 'vue'


const location = ref('')
const weatherData = ref(null)

async function searchWeather() {
  const response = await fetch(`https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${location.value}?unitGroup=us&key=3C8TRCWYPKSPU83H6U8CJ5CUR&contentType=json`);
  const data = await response.json();
  weatherData.value = data.days;
  console.log(data.days)
}


</script>

<template>
<div class="weather-search">
<div class="search_bar">
  <h2>Weather Search</h2>
  <div>
  <input type="text" v-model="location" placeholder="Enter location" />
  </div>
  <div> <button @click="searchWeather">Search</button></div>
 
  </div>
<div class="table-responsive">
  <table class="weather-table" v-if="weatherData">
    <thead>
      <tr>
        <th>Time</th>
        <th>Temperature (&deg;F)</th>
        <th>Feels Like (&deg;F)</th>
        <th>Humidity (%)</th>
        <th>Dew Point (&deg;F)</th>
        <th>Wind Speed (mph)</th>
        <th>Wind Gust (mph)</th>
        <th>Wind Direction (&deg;)</th>
        <th>Pressure (mb)</th>
        <th>Visibility (mi)</th>
        <th>Cloud Cover (%)</th>
      </tr>
    </thead>
    <tbody>
      <!-- Use Vue.js to loop through each hour and populate table rows -->
      <tr v-for="(hour, index) in weatherData" :key="index">
        <td>{{ hour.datetime }}</td>
        <td>{{ hour.temp }}</td>
        <td>{{ hour.feelslike }}</td>
        <td>{{ hour.humidity }}</td>
        <td>{{ hour.dew }}</td>
        <td>{{ hour.windspeed }}</td>
        <td>{{ hour.windgust }}</td>
        <td>{{ hour.winddir }}</td>
        <td>{{ hour.pressure }}</td>
        <td>{{ hour.visibility }}</td>
        <td>{{ hour.cloudcover }}</td>
      </tr>
    </tbody>
  </table>
</div>

</div>
</template>

<style scoped>
.weather-search {
  margin: 20px;


}

.search_bar{
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  column-gap:20px;
  row-gap:20px;
}
.weather-search input[type='text'] {
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.weather-search button {
  padding: 8px 65px;
  font-size: 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.weather-search button:hover {
  background-color: #0056b3;
}

.table-responsive {
  overflow-x: auto;
  margin:40px 0;
}

.weather-table {
  width: 100%;
  border-collapse: collapse;
}

.weather-table th,
.weather-table td {
  padding: 8px;
  text-align: center;
  border: 1px solid #ddd;
}

.weather-table th {
  background-color: #f2f2f2;
}

/* Responsive styles */
@media screen and (max-width: 767px) {
  .table-responsive {
    overflow-x: scroll;
  }
}

</style>
