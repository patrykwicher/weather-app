<template>
<div id='input-div'>
  <input type='text' id='input' name='city' placeholder="Find a city!" v-model="inputVariable" @keypress.enter="inputCapturing()">
  <button @click="inputCapturing" id="submit-button">Submit</button>
</div>
</template>

<script>
export default {
  name: 'Input',
  data() {
    return {
      inputVariable: '',
    }
  },
  methods: {
    inputCapturing() {
      if (this.inputVariable === '') alert("Input can not be empty");
      else if (!isNaN(this.inputVariable)) alert('Wrong input')
      else {
        // $emit("nazwa eventu", argument, który chcemy przepuścić)
        this.$emit("inputCapturing", this.inputVariable);
        this.inputVariable = '';
      }
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Epilogue&display=swap');

@media (min-width: 1300px) {
  #input-div {
    font-family: 'Epilogue', sans-serif;
    display: flex;
  }

  #input {
    border-radius: 5px;
    padding-left: 0.5%;
    width: 30vw;
    padding: 0.6vw;
    font-size: 1em;
    border: none;
    opacity: 0.5;
    box-shadow: 3px 3px 2px #4f6377;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    border-radius: 5px;
    background-color: white;
    padding: 0.75vw;
    margin-left: 1vw;
    opacity: 0.5;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
  }

  #submit-button:active {
    opacity: 0.8;
  }
}

@media (max-width: 600px) {
    #input {
      border-radius: 5px;
      padding-left: 0.5%;
      width: 30vw;
      padding: 0.6vw;
      font-size: 1em;
      border: none;
      opacity: 0.5;
      box-shadow: 3px 3px 2px #4f6377;
    }

    #input:focus {
      opacity: 0.8;
    }

    #submit-button {
      border: none;
      border-radius: 5px;
      background-color: white;
      padding: 0.75vw;
      opacity: 0.5;
      font-family: 'Epilogue', sans-serif;
      box-shadow: 3px 3px 2px #4f6377;
      margin-top: 1vh;
      width: 31.5vw;
    }

    #submit-button:active {
      opacity: 0.8;
    }
}

@media (min-width: 600px) {
  #input {
    border-radius: 5px;
    padding-left: 0.5%;
    width: 30vw;
    padding: 0.6vw;
    font-size: 1em;
    border: none;
    opacity: 0.5;
    box-shadow: 3px 3px 2px #4f6377;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    border-radius: 5px;
    background-color: white;
    padding: 0.75vw;
    opacity: 0.5;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
    margin-top: 1vh;
    width: 31.5vw;
  }

  #submit-button:active {
    opacity: 0.8;
  }
}

@media (min-width: 992px) {
  #input-div {
    font-family: 'Epilogue', sans-serif;
    display: flex;
  }

  #input {
    border-radius: 5px;
    padding-left: 0.5%;
    width: 25vw;
    padding: 0.6vw;
    font-size: 1em;
    border: none;
    opacity: 0.5;
    box-shadow: 3px 3px 2px #4f6377;
    margin-left: 1.7vw;
    margin-top: 1vh;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    border-radius: 5px;
    background-color: white;
    padding: 0.75vw;
    margin-left: 1vw;
    opacity: 0.5;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
    width: 8vw;
    height: 7vh;
  }

  #submit-button:active {
    opacity: 0.8;
  }
}
</style>
