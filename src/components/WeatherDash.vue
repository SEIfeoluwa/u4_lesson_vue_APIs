<template>
  <section class="current">
    <h3>Current Weather</h3>
    <div>
      <h4>{{ Math.ceil(currentWeather.feels_like) }}&#176;</h4>
      <p>{{ currentWeather.weather[0].description }}</p>
      <img :src="generateIconUrl(currentWeather.weather[0].icon)" />
    </div>
  </section>
</template>

<script>
  export default {
    name: 'WeatherDash',
    props: ['currentWeather'],
    methods: {
      generateIconUrl(ico) {
        return `http://openweathermap.org/img/wn/${ico}@2x.png`
      }
    }
  }
</script>

<style>
  .current {
    background-color: rgb(229, 234, 255);
    width: 200px;
    border: 2px solid rgb(139, 139, 139);
  }
</style>