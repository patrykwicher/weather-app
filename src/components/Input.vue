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
      else if (!isNaN(this.inputVariable)) alert('Wrong input');
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

@media (max-width: 688px) {
  #input-div {
    display: flex;
    flex-direction: column;
  }

  #input {
    border-radius: 5px;
    width: 90vw;
    margin: 0 auto 0 auto;
    padding: 2vw;
    font-size: 1em;
    border: none;
    opacity: 0.5;
    box-shadow: 3px 3px 2px #4f6377;
    font-family: 'Epilogue', sans-serif;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    border-radius: 5px;
    padding: 2vw;
    opacity: 0.5;
    font-size: 1em;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
    margin: 1vh auto 0 auto;
    width: 94vw;
  }

  #submit-button:active {
    opacity: 0.8;
  }
}

@media (min-width: 689px) {
  #input-div {
    display: flex;
    margin-bottom: 3vh;
  }

  #input {
    font-family: 'Epilogue', sans-serif;
    border-radius: 5px;
    width: 70vw;
    margin: 0 0 0 auto;
    padding: 2vw;
    font-size: 1em;
    border: none;
    opacity: 0.5;
    box-shadow: 3px 3px 2px #4f6377;
    transition: .5s;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    background-color: white;
    border-radius: 5px;
    padding: 0.75vw;
    margin: 0 auto 0 1vw;
    opacity: 0.5;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
    transition: .5s;
    width: 15vw;
  }

  #submit-button:active {
    opacity: 0.8;
  }
}

@media (min-width: 992px) {
  #input-div {
    font-family: 'Epilogue', sans-serif;
    display: flex;
    margin-bottom: 5vh;
  }

  #input {
    border-radius: 5px;
    padding-left: 1.5vw;
    width: 70vw;
    margin: 0 0 0 4vw;
  }

  #input:focus {
    opacity: 0.8;
  }

  #submit-button {
    border: none;
    border-radius: 5px;
    background-color: white;
    padding: 0.75vw;
    margin: 0 4vw 0 1vw;
    opacity: 0.5;
    font-family: 'Epilogue', sans-serif;
    box-shadow: 3px 3px 2px #4f6377;
    width: 15vw;
    font-size: 2vw
  }

  #submit-button:active {
    opacity: 0.8;
  }
}

@media (min-width: 3840px) {
  #input {
    font-size: 2vw; 
  }
}

</style>
