<template>
<div id="app" :style="bgColor">
  <Input v-on:inputCapturing="fetchData($event)" />
  <Result v-bind:weather="weather" />
</div>
</template>

<script>
// import Header from './components/Header.vue'
import Input from './components/Input.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  data() {
    return {
      city: '',
      apiKey: '&appid=b2cfc3526743b036459d865a76cc2f1e',
      url: `https://api.openweathermap.org/data/2.5/weather?q=`,

      weather: {},
      error: null,
      bgColor: {
        backgroundColor: '',
        color: ''
      },
    }
  },
  methods: {
    returnUrl() {
      return `${this.url}${this.city}&units=metric${this.apiKey}`;
    },
    //fetchData($event - argument, który emitujemy do App.vue z Input.vue)
    fetchData(inputValue) {
      this.city = inputValue;
      let url = this.returnUrl();
      fetch(url)
        .then(response => response.json())
        .then(response => {
          this.weather = response;
          this.changeBackgroundColor();
        })
        .catch(error => {
          this.weather = error;
        })
    },
    changeBackgroundColor() {
      if (this.weather.cod === 200) {
        if (this.weather.weather[0].main === 'Rain') this.bgColor.backgroundColor = '#7491af'
        else if (this.weather.weather[0].main === 'Thunderstorm') this.bgColor.backgroundColor = '#8B7BAA'
        else if (this.weather.weather[0].main === 'Clear') this.bgColor.backgroundColor = '#FEB48F'
        else if (this.weather.weather[0].main === 'Clouds') this.bgColor.backgroundColor = '#b2d4f7'
        else if (this.weather.weather[0].main === 'Mist') this.bgColor.backgroundColor = '#99a7ad'
        else if (this.weather.weather[0].main === 'Snow') {
          this.bgColor.backgroundColor = '#E0E7EA'
          this.color = '#7C959D'
        }
      }
      else if (this.weather.cod === '404') {
        this.bgColor.backgroundColor = '#BBB'
      }
    }
  },
  components: {
    // Header,
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
