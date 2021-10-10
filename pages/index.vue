<template>
  <div class="app">
    <div class="search-box">
      <input
        type="text"
        class="search-bar"
        placeholder="your city..."
        v-model="query"
        @keypress="fetchWeather"
      />
    </div>

    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
        <div class="weather">{{ weather.weather[0].main }}</div>
      </div>

      <NuxtLink to="/textarea">next page</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      api_key: '5e9769967e9442fc426d2fbac49e9edd',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
    }
  },
  methods: {
    async fetchWeather(e) {
      if (e.key == 'Enter') {
        await this.$axios
          .$get(
            `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
          )
          .then(this.setResults)
      }
    },
    setResults(results) {
      this.weather = results
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  background-color: #e3e3e3;
  min-height: 100vh;
  padding: 25px;
  text-align: center;
  transition: 0.4s;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-bar {
  width: 50%;
  margin: 0 auto;
  display: block;
  border: none;
  outline: none;
  padding: 10px;
  border-radius: 15px;
}
.location {
  color: rgb(51, 51, 51);
  font-size: 48px;
}
.temp {
  display: inline-block;
  padding: 10px 25px;
  color: rgb(51, 51, 51);
  font-size: 102px;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather {
  color: rgb(51, 51, 51);
  font-size: 48px;
  font-style: italic;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
</style>
