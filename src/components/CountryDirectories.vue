<template>
<div class="cd">
<div class="container">
<nav class="navbar">
  <a class="navbar-brand mx-auto" href="/">
    <img src="../assets/logo.png" width="50" height="50" alt="" loading="lazy">  Countries
  </a>
</nav>
<div class="row">
<div class="col-sm top">
<div>
    <label>Pick a Country</label>
    <select name="countries" id="countries" v-model="selectedCountry" @change="onCountrySelect($event)" class="custom-select custom-select-lg mb-3">
      <option :value=country.name v-for="country in countries" :key="country.id" class="count-option">{{ country.name }}</option>
    </select>
</div>

<div> 
    <label>Pick a State</label>
    <select name="states" id="states" v-model="selectedState" @change="onStateSelect($event)" class="custom-select custom-select-lg mb-3">
      <option :value="state.name" v-for="state in states" :key="state.id" class="count-option">{{ state.name }}</option>
    </select>
     <div v-if="stateError" :class="{ empty: stateError }" class="alert alert-warning" role="alert">
      This Country Has No States!
    </div>
</div>

<div>
    <label>Pick a City</label>
    <select name="cities" id="cities" v-model="selectedCity" class="custom-select custom-select-lg mb-3">
      <option :value="city.name" v-for="city in cities" :key="city.id" class="count-option">{{ city.name }}</option>
    </select>
     <div  v-if="cityError" :class="{ empty: cityError }" class="alert alert-warning" role="alert">
      This State Doesn't Have Any City!
    </div>
</div>
</div>
<div class="col-sm top">
  <div class="options">
    <p v-if="selectedCountry"><span class="head">Country:</span> {{ selectedCountry }}</p>
    <p v-if="selectedState"><span class="head">State:</span> {{ selectedState }}</p>
    <p v-if="selectedCity"><span class="head">City:</span> {{ selectedCity }}</p>
  </div>
</div>

</div>
</div>
</div>
</template>

<script>
export default {
  name: 'CountryDirectories',
   data() {
     return {
      selectedCountry: "",
      selectedState: "",
      selectedCity: "",
      stateError: false,
      cityError: false,
      countries: [],
      states: [],
      cities: []
      }
    },
    created() {
      this.$http.get('https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json').then(
        response=> {
          return response.json()
          })
        .then(data=> {
          this.countries = data.slice(0, 251);
        })    
    },
    methods: {
        onCountrySelect(event) {
            const state = event.target.value
            const index = this.countries.findIndex((x=>x.name === state))
            const countryState = this.countries[index]['states']
            if (countryState.length === 0) {
                this.stateError = !this.stateError 
                this.states = null   
                this.cities = ""
            } else {
                this.states = countryState
                this.stateError = false
            }
        },
        onStateSelect(event) {
            const state = event.target.value
            const index = this.states.findIndex((x=>x.name === state))
            const city = this.states[index]['cities']
            if (city.length === 0) {
                this.cityError = !this.cityError
            } else {
                this.cities = city
                this.cityError = false
            }
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');

.top{
  margin-top: 4rem;
}
.custom-select{
  color: #151515;
  font-family: 'Poppins', sans-serif;
}

label{
  font-family: 'Poppins', sans-serif;
  font-weight: 600;
  color: #63c069;
  font-size: 1.5rem;
}

.head{
  font-family: 'Poppins', sans-serif;
  font-weight: bold;
  color: #63c069;
  font-size: 1.25rem;
}


.options {
    font-size: 1.25rem;
    font-weight: 600;
}

.navbar-brand{
  font-size: 1.1rem;
  font-family: 'Poppins', sans-serif;
  font-weight: 600;
  color: #63c063;
}

</style>
