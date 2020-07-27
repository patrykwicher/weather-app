<template>
<div id="app" :style="bgColor">
  <Input v-on:inputCapturing="fetchDataByAsync($event)" />
  <Result v-bind:weather="weather" />
</div>
</template>

<script>
import Input from './components/Input.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  data() {
    return {
      city: '',
      apiKey: '&appid=b2cfc3526743b036459d865a76cc2f1e',
      temperatureUrl: `https://api.openweathermap.org/data/2.5/weather?q=`,
      forecastUrl: `https://api.openweathermap.org/data/2.5/forecast?q=`,
      weather: {
        temperature: {},
        forecast: {}
      },
      error: null,
      bgColor: {
        backgroundColor: '',
        color: ''
      },
      forwardForecasts: null,
    }
  },
  methods: {
    returnUrl() {
      return [`${this.temperatureUrl}${this.city}&units=metric${this.apiKey}`, `${this.forecastUrl}${this.city}&units=metric${this.apiKey}&cnt=5`];
    },
    // async function - zwraca Promise
    async fetchDataByAsync(inputValue) {
      this.city = inputValue;
      let urls = this.returnUrl();
      // jeżeli w bloku try pojawi się jakiś błąd, zostanie on przeakazany i obsłużony w catch
      try {
        // await pozwala na natychmiastowe odczytanie wartości z obietnicy, bez bawienia się w łańcuszek .then(...)
        let temperatureResponse = await fetch(urls[0]);
        this.weather.temperature = await temperatureResponse.json();
        let forecastReponse = await fetch(urls[1]);
        this.weather.forecast = await forecastReponse.json();
        this.changeBackgroundColor();
      }
      catch(error) {
        this.temperature = error;
      }

    },

    changeBackgroundColor() {
      if (this.weather.temperature.cod === 200) {
        if (this.weather.temperature.weather[0].main === 'Rain') this.bgColor.backgroundColor = '#7491af'
        else if (this.weather.temperature.weather[0].main === 'Thunderstorm') this.bgColor.backgroundColor = '#8B7BAA'
        else if (this.weather.temperature.weather[0].main === 'Clear') this.bgColor.backgroundColor = '#FEB48F'
        else if (this.weather.temperature.weather[0].main === 'Clouds') this.bgColor.backgroundColor = '#b2d4f7'
        else if (this.weather.temperature.weather[0].main === 'Mist') this.bgColor.backgroundColor = '#99a7ad'
        else if (this.weather.temperature.weather[0].main === 'Snow') {
          this.bgColor.backgroundColor = '#E0E7EA'
          this.color = '#7C959D'
        }
      }
      else if (this.weather.temperature.cod === '404') {
        this.bgColor.backgroundColor = '#BBB'
      }
    },
    amountOfForecasts() {
      // const width = window.innerWidth;
      // const height = window.innerhHeight;
      // if(width === 834) this.forwardForecasts = 4;
    }
  },
  mounted() {
    this.amountOfForecasts();
  },
  components: {
    Input,
    Result
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Epilogue&display=swap');

/* font-family: 'Epilogue', sans-serif; */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0 30vw 0 30vw;
  background-color: #BBB;
  padding: 2vh 0 0 0;
  color: white;
  font-family: 'Epilogue', sans-serif;
  height: 90vh;
  border-radius: 10px;
  transition: .5s;
  box-shadow: 4px 4px 10px #5f7994;
}

::-moz-selection {
  color: none;
  background: none;
}
</style>
