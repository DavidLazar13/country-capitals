<template>
  <div id="app">
    <img src="./assets/earth.png">
    <h1>Guess the capital of:</h1>
    <h2>{{country.name}}</h2>
    <input type="text"
           id="capital"
           v-model="inputCapital">
    
    </input>



    <button @click="checkCapital">
        Check
    </button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      country: {},
      inputCapital: "",
      status: "",
      correctCapital: ""

    }
  },
  mounted () {
    this.getData()
  },
  methods:{
      getData() {
        fetch('https://restcountries.eu/rest/v2/all')
      .then(
        (response) => {
          if (response.status !== 200) {
            console.log('Looks like there was a problem. Status Code: ' +
              response.status);
            return;
          }

          // Examine the text in the response
          response.json().then( data => {
            console.log(data);
            const numberOfCountries = data.length
            const randomCountryIndex = Math.floor(Math.random() * numberOfCountries)
            console.log(data[randomCountryIndex])
            this.country = data[randomCountryIndex]
          });
        }
      )
      .catch(function(err) {
        console.log('Fetch Error :-S', err);
      });
      },
      
      checkCapital(){
        var countryCapital = this.country.capital
        var inputCapital = this.inputCapital
        if (inputCapital === countryCapital){
          console.log('yay')
          this.status = true
        } else {
          console.log('nay')
          this.status = false
          }
      }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
