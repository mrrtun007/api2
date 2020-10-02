<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input
          v-model="query"
          type="text"
          class="search-bar"
          placeholder="Search..."
          @keypress="fetchWeather"
        >
      </div>

      <div v-if="typeof weather.main != 'undefined'" class="weather-wrap">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">
            {{ dateBuilder() }}
          </div>
        </div>
        <div class="weather-box">
          <div class="temp">
            {{ Math.round(weather.main.temp) }}°c
            <br>{{ weather.main.temp_min }} min /
            {{ weather.main.temp_max }} max
          </div>
          <div class="weather">
            {{ weather.weather[0].main }}
          </div>
        </div>
        <nuxt-link :to=" {name: 'product-id', params: { id: weather }} ">
          <v-btn>Details</v-btn>
        </nuxt-link>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      api_key: 'e406d5e840c922e69b038ec4c507ebc2',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      // eslint-disable-next-line eqeqeq
      if (e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then((res) => {
            return res.json()
          }).then(this.setResults)
      }
    },
    setResults (results) {
      this.weather = results
    },
    dateBuilder () {
      const d = new Date()
      const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
      const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']

      const day = days[d.getDay()]
      const date = d.getDate()
      const month = months[d.getMonth()]
      const year = d.getFullYear()

      return `${day} ${date} ${month} ${year}`
    },
    time () {
      const time = new Date()
      const t = ['1']
      const timezone = time[t.gettime()]
      return `${timezone}`
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('https://www.zoomcamera.net/wp-content/uploads/2019/06/jimmy-conover-383739.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm {
  background-image: url('https://www.zoomcamera.net/wp-content/uploads/2019/06/amber-teasley-358290.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;

  appearance: none;
  border:none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: rgb(244, 245, 244);
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: rgb(30, 7, 208);
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
