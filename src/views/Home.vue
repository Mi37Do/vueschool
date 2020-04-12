<template>
  <div class="home">
    <main>
      <v-card height="300px"
              width="600px"
              class="mx-auto"
              align="center">
      <div class="search-box">
        <v-text-field
                type="text"
                class="search-bar"
                placeholder="Search..."
                v-model="query"
                @keypress="fetchWeather"
       ><v-icon slot="append">mdi-magnify</v-icon>
        </v-text-field>
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <v-row
                class="mb-6"
                no-gutters
        >
          <v-col
          >
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
          </v-col>
          <v-col justify="center">
        <div class="location-box">
          <v-img src="src/assets/logo.png"></v-img>
          <div class="location" >{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>

        </div>
          </v-col>
        </v-row>
        <v-divider></v-divider>

      </div>
      </v-card>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
    name: 'Home',
    data () {
      return {
        api_key: '8e3ab3e2f1f6e56e58c9add1636abeed',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        query: '',
        weather: {}
      }
    },
    methods: {
      fetchWeather (e) {
        if (e.key == "Enter") {
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
                  .then(res => {
                    return res.json();
                  }).then(this.setResults);
        }
      },
      setResults (results) {
        this.weather = results;
      },
      dateBuilder () {
        let d = new Date();
        let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();
        return `${day} ${date} ${month} ${year}`;
      }
    }
  }
</script>

<style scoped>
.search-bar{
  width: 250px;
}
.location-box .date {
  color: #2b2b2b;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #2b2b2b;
  font-size: 102px;
  font-weight: 900;
  border-radius: 16px;

}
</style>