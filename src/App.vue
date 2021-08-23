<template>
  <div class="d-flex justify-content-center">
    <div class="card" style="width: 18rem">
    <img src="./assets/city.jpg" class="card-img-top" alt="city" />
    <div class="card-body">
      <div class="input-group mb-3">
        <button class="btn btn-success" type="button" id="button-addon1" @click="getData">search</button>
        <input type="text" 
          v-model="city"
          class="form-control" 
          placeholder="city name" 
          aria-label="Example text with button addon" 
          aria-describedby="button-addon1">
      </div>
      <div class="card-text" v-if="data">
        <p> City name: {{data.name}} </p>
        <p>Temp: {{ data.main.temp }} C</p>
        <p>description : {{ data.weather[0].description }}</p>
      </div>
      <div
       class="card-text" 
       v-else-if="isLoading">
        Loading ... 
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
const API_KEY = '4148eba9fcabd4c276eccc1b25bf33cc';
export default{
  name: "App",
  data: () => ({
    city: '',
    data: null,
    isLoading : false,
  }),

  methods:{
    getData(){
      this.isLoading = true
      axios.get(`https://api.openweathermap.org/data/2.5/weather` , {
        params:{
          q: this.city,
          appid: API_KEY,
          units: 'metric',
          lang: 'fa'
        }
      }).then(({data}) => {
        this.isLoading = false
        this.data = data
      })
    }

  }
}

</script>

<style>

</style>
