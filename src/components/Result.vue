<template>
<div id="result-window">
  <div v-if="weather.cod === 200" id="wrapper">
    <div class="first-row">
      <div class="city-date" id="city" :removeVoivodeship="removeVoivodeship()"><span class='box-shadow'> {{ weather.name }} </span></div>
      <div class="city-date" id="date"><span class='box-shadow'><sup> {{ weekDays[date.getDay()-1] }} {{ date.getDate() }} {{ months[date.getMonth()] }} {{ date.getFullYear() }} </sup></span></div>
    </div>
    <div id="weather-icon" class='box-shadow'>
      <img :src="returnIconUrl()" />
    </div>
    <div id="weather-type" class='box-shadow'> {{ weather.weather[0].main }} </div>
    <div id="temperature-container" class='box-shadow'>
      <div id='temperature-text'>{{ Math.round(weather.main.temp) }} <sup>o</sup>C</div>
    </div>
  </div>
  <div v-else class="box-shadow" id="error"> {{ weather.message }} </div>
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
      return `${this.iconUrl}${this.weather.weather[0].icon}@2x.png`;
    },
    removeVoivodeship() {
      if (this.weather.name === 'Lublin Voivodeship' || this.weather.name === 'Łódź Voivodeship' || this.weather.name === 'Opole Voivodeship') {
        let shortenedName = this.weather.name.split(" ")
        return this.weather.name = shortenedName[0];
      } else this.weather.name;
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

  .first-row {
    display: flex;
    justify-content: space-around;
    font-size: 1.3em;
  }

  #temperature-container {
    font-size: 2em;
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

  #result-window, #error{
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

  #result-window, #error{
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
