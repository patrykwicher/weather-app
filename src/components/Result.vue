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
        <div id='forecast-icon'>
          <img :src="`${iconUrl}${forecast.weather[0].icon}@2x.png`" />
        </div>
        <div class="forecast-temp"> {{ Math.round(forecast.main.temp) }} <sup>o</sup>C </div>
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
@media (max-width: 688px) {
  .wrapper {
    display: flex;
    flex-direction: column;
  }

  #result-window,
  #error {
    margin-top: 4vh;
    font-size: 10vw;
  }

  #city {
    font-size: 11vw;
    margin-bottom: 2vh;
  }

  #date {
    font-size: 6vw;
  }

  #weather-icon {
    transform: scale(1.5, 1.5);
  }

  #weather-type {
    margin-top: -0.8vh;
    font-size: 7vw;
    margin-bottom: 1vh;
  }

  #temperature-text {
    font-size: 10vw;
  }

  .box-shadow {
    text-shadow: 3px 3px 1px #4f6377;
  }

  #forecast-wrapper {
    display: flex;
    font-size: 3.5vw;
    justify-content: space-evenly;
    background-color: #8599ad;
    padding: 2vh 0 1vh 0;
    margin: 3vh 4vw 1vh 4vw;
    border-radius: 10px;
    flex-wrap: wrap;
  }

  #forecas-temp {
    margin-bottom: 3vh;
  }
}

@media (min-width: 689px) {
  #result-window {
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
    display: block;
    font-size: 1.3em;
  }

  #temperature-container {
    font-size: 1.6em;
    border-radius: 10px;
  }

  #temperature-text {
    opacity: 0.9;
    font-size: 6vw;
  }

  #city {
    font-size: 10vw;
    margin-top: 4vh;
  }

  #date {
    font-size: 5vw;
    margin: 2vh 0 2vh 0;
  }

  #weather-icon {
    transform: scale(2, 2);
  }

  #weather-type {
    font-size: 4vw;
    margin: 3vh 9vw 3vh 9vw;
  }

  .box-shadow {
    text-shadow: 3px 3px 1px #4f6377;
  }

  #forecast-wrapper {
    width: 85vw;
    margin: 4vh auto 0 auto;
    font-size: 2.5vw;
  }

  #error {
    font-size: 7vw;
    margin-top: 4vh;
  }

  #forecast-icon {
    transform: scale(1.2, 1.2)
  }
}

@media (min-width: 992px) {
  .first-row {
    display: flex;
    justify-content: space-evenly;
    margin-bottom: 6vh;
  }

  #city {
    font-size: 8vw;
    margin-top: 1vh;
  }

  #date {
    font-size: 4vw;
  }

  #forecast-wrapper {
    width: 90vw;
    margin-top: 1.5vh;
  }

  #weather-icon {
    margin: -5vh auto 2vh auto;
  }

  #temperature-text, #weather-type {
    margin: 1vh auto 1vh auto;
  }
}

@media (min-width: 1280px) {
  #city {
    font-size: 7vw;
  }

  #date {
    font-size: 4vw;
  }

  #weather-icon {
      transform: scale(2, 2);
      margin-top: -5vh;
  }

  #weather-type {
    font-size: 3.5vw;
    margin: 2vh auto 2vh auto;
  }

  #temperature-text {
    font-size: 5.5vw;
    margin: 1vh auto 3vh auto;
  }
}

@media (min-width: 3840px) {
  #weather-icon {
    transform: scale(4,4);
    margin-bottom: 8vh;
  }
}
</style>
