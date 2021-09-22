<template>
  <div id="app">
    <WeatherDash v-if="currentWeather" :currentWeather="currentWeather" />
    <WeeklyForecast v-if="currentWeather" :weeklyForecast="dailyWeather" />
    <div v-else>
      <h3>No Weather</h3>
    </div>
  </div>
</template>

<script>
import WeatherDash from './components/WeatherDash.vue'
import WeeklyForecast from './components/WeeklyForecast.vue'
import axios from 'axios'
const API_KEY = process.env.VUE_APP_WEATHER_KEY
export default {
  name: 'App',
  components: {
    WeatherDash,
    WeeklyForecast
  },
  data: () => ({
    dailyWeather: [],
    currentWeather: null
  }),
  mounted: function() {
    navigator.geolocation.getCurrentPosition(async ({ coords }) => {
      await this.getCurrentWeather(coords)
    })
  },
  methods: {
    async getCurrentWeather(coords) {
      const res = await axios.get(
        `https://api.openweathermap.org/data/2.5/onecall?lat=${coords.latitude}&lon=${coords.longitude}&units=imperial&appid=${API_KEY}`
      )
      this.currentWeather = res.data.current
      this.dailyWeather = res.data.daily
    },
    async get4DayForecast() {}
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
