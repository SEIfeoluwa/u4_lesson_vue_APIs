<template>
  <section>
    <h2>Weekly Forecast</h2>
    <div class="items">
      <div class="day" v-for="(data, index) in weeklyForecast" :key="index">
        <h2>{{ generateDay(data.dt) }}</h2>
        <p>{{ generateDate(data.dt) }}</p>
        <h3>{{ Math.ceil(data.feels_like.day) }}&#176;</h3>
        <p>{{ data.weather[0].description }}</p>
        <img :src="generateIconUrl(data.weather[0].icon)" />
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'WeeklyForecast',
    props: ['weeklyForecast'],
    methods: {
      generateIconUrl(ico) {
        return `http://openweathermap.org/img/wn/${ico}@2x.png`
      },
      generateDay(dt) {
        const days = [
          'Sunday',
          'Monday',
          'Tuesday',
          'Wednesday',
          'Thursday',
          'Friday',
          'Saturday'
        ]
        let date = new Date(dt * 1000)
        let day = date.getDay()
        return days[day]
      },
      generateDate(dt) {
        let dateTime = new Date(dt * 1000)
        let dateStr = dateTime.toDateString().split(' ')
        dateStr.splice(0, 1)
        dateStr.splice(dateStr.length - 1)
        return dateStr.join(' ')
      }
    }
  }
</script>

<style>
  section {
    width: 100vw;
  }
  
  .items {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .day {
    margin: 2px;
    background-color: rgb(234, 234, 234);
    width: 150px;
    border: 2px solid rgb(139, 139, 139);
  }
</style>
