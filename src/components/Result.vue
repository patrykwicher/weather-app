<template>
<div id="result-window">
  <div v-if="weather.temperature.cod === 200" id="wrapper">
    <div class="first-row">
      <div class="city-date" id="city" :removeVoivodeship="removeVoivodeship()"><span class='box-shadow'> {{ weather.temperature.name }} </span></div>
      <div class="city-date" id="date"><span class='box-shadow'><sup> {{ weekDays[date.getDay()-1] }} {{ date.getDate() }} {{ months[date.getMonth()] }} {{ date.getFullYear() }} </sup></span></div>
    </div>
    <div id="weather-icon" class='box-shadow'>
      <img :src="returnIconUrl()" />
    </div>
    <div id="weather-type" class='box-shadow'> {{ weather.temperature.weather[0].main }} </div>
    <div id="temperature-container" class='box-shadow'>
      <div id='temperature-text'>{{ Math.round(weather.temperature.main.temp) }} <sup>o</sup>C</div>
    </div>
    <div id='forecast-wrapper' class='box-shadow'>
    <div v-for="forecast in weather.forecast.list" :key="forecast.dt" id="hour-wrapper">
        <div> {{ forecast.dt_txt.split(" ")[1].split(":")[0] }}:00 </div>
        <div>
          <img :src="`${iconUrl}${forecast.weather[0].icon}@2x.png`" />
        </div>
        <div> {{ Math.round(forecast.main.temp) }} <sup>o</sup>C </div>
    </div>
  </div>
  </div>
  <div v-else class="box-shadow" id="error"> {{ weather.temperature.message }} </div>
</div>
</template>

<script>
export default {
  name: 'ResultWindow',
  props: {
    weather: {
      type: Object,
    }
  },
  data() {
    return {
      date: new Date(),
      weekDays: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
      months: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
      iconUrl: `http://openweathermap.org/img/wn/`,
    }
  },
  methods: {
    returnIconUrl() {
      return `${this.iconUrl}${this.weather.temperature.weather[0].icon}@2x.png`;
    },
    removeVoivodeship() {
      if (this.weather.temperature.name === 'Lublin Voivodeship' || this.weather.temperature.name === 'Łódź Voivodeship' || this.weather.temperature.name === 'Opole Voivodeship') {
        let shortenedName = this.weather.temperature.name.split(" ")
        return this.weather.temperature.name = shortenedName[0];
      } else this.weather.temperature.name;
    },
  },
}
</script>

<style scoped>
@media (min-width: 1300px) {
  #result-window {
    opacity: 0.8;
    margin-top: ;
  }

  #forecast-wrapper {
    display: flex;
    justify-content: space-evenly;
    margin-top: 2vh;
    text-shadow: 1.5px 1.5px #4f6377;
    background-color: #8599ad;
    padding: 2vh 0 2vh 0;
    margin: 2vh 1vw 4vh 1vw;
    border-radius: 10px;
  }

  #hour-wrapper {
      opacity: 1;
  }

  .first-row {
    display: flex;
    justify-content: space-around;
    font-size: 1.3em;
  }

  #temperature-container {
    font-size: 1.6em;
    border-radius: 10px;
  }

  #temperature-text {
    opacity: 0.9;
  }

  #city {
    font-size: 2em;
  }

  #weather-icon {
    transform: scale(1.5, 1.5);
    opacity: 1;
  }

  #weather-type {
    font-size: 2em;
    margin: 0 9vw 3vh 9vw;
  }

  .box-shadow {
    text-shadow: 3px 3px 1px #4f6377;
  }

  #error {
    font-size: 2em;
  }
}

@media (max-width: 600px) {
  .wrapper {
    display: flex;
    flex-direction: column;
  }

  #result-window,
  #error {
    margin-top: 7vh;
  }

  #city {
    font-size: 2.5em;
    margin-bottom: 2vh;
  }

  #date {
    font-size: 1.2em;
  }

  #weather-type {
    margin-top: -2vh;
    font-size: 1.5em;
    margin-bottom: 1vh;
  }

  #temperature-text {
    font-size: 3em;
  }

  .box-shadow {
    text-shadow: 3px 3px 1px #4f6377;
  }
}

@media (min-width: 600px) {
  .wrapper {
    display: flex;
    flex-direction: column;
  }

  #result-window,
  #error {
    margin-top: 7vh;
  }

  #city {
    font-size: 2.5em;
    margin-bottom: 2vh;
  }

  #date {
    font-size: 1.2em;
  }

  #weather-type {
    margin-top: -2vh;
    font-size: 1.5em;
    margin-bottom: 1vh;
  }

  #temperature-text {
    font-size: 3em;
  }

  .box-shadow {
    text-shadow: 3px 3px 1px #4f6377;
  }
}
</style>
