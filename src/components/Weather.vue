<template>
  <div id="app">
    <div class="mainn" v-bind:class="{warm: state_weather}">
        <div class="search-box">
           <input class="search-bar" type="text" placeholder="Wpisz miejscowość..." v-model="data.city" @keyup.enter="getApi()">
        <div v-if="data.weather">
          <div class="header">
           <h1>{{data.weather.name}}</h1>
           <h3>{{ new Date().toLocaleString() }}</h3>
         </div>
         <div class="temp">
            <h2>{{Math.round(data.weather.main.temp)}}&deg;</h2>
         </div>
         <div class="state">
            <h3>{{ data.weather.weather[0].main}}</h3>
        </div>
      </div>
    </div>
  </div>
</div>
</template>
  
<script>
import axios from "axios"
export default {
  name: 'weather-item',
  data(){
    return{
     data:{
      city:'',
      weather: null,
      current_day:'',
      state_weather:false
    }
  }
},
mounted: async function(){
    this.getApi()
},
methods:{
  async getApi(){
    const getWeather = await axios.get(`https://api.openweathermap.org/data/2.5/weather?units=metric&q=${this.data.city}&appid=614da9d80f482543a8babb97e7ebda08`)
    console.log(getWeather);
    this.data.weather = getWeather.data
    this.data.city = ''
    if(this.data.weather.main.temp > 16){
          this.state_weather = true
      }else{
        this.state_weather = false
      }
            }
    }
  }
</script>
  
<style scoped>
*{
  margin: 0;
  padding: 0;
  }
body{
    font-family: sans-serif;
  }
  #app{
  background: linear-gradient(rgba(32, 31, 31, 0.438), rgba(185, 194, 186, 0)), url('../assets/pogoda.jpg') no-repeat;
    height: 98.5vh;
    background-position: center;
    background-size: cover;
    letter-spacing: 1px;
    display:flex;
  }
.mainn{
  border-radius: 5px;
    padding: center;
    font-weight: 800;
    text-align: center;
    margin: auto auto;
}
.search-box{
  border-radius: 5px;
    padding: center;
    font-weight: 800;
    text-align: center;
}
.search-box .search-bar{
  display: block;
  width: 70%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 16px;
}
.temp{
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
}
.header{
  padding-top: 20px;
  font-size: 20px;
  color: azure;
}
.state{
  position: absolute;
  color: #FFF;
  font-size: 48px;
  font-style: italic;
  text-align: center;
}
@media only screen and (max-width: 1550px) {
  #app {
    background: linear-gradient(rgba(32, 31, 31, 0.438), rgba(185, 194, 186, 0)), url('../assets/niebieskie.jpg') no-repeat;
  }
}
@media only screen and (max-height: 700px) {
  #app {
    background: linear-gradient(rgba(32, 31, 31, 0.438), rgba(185, 194, 186, 0)), url('../assets/niebieskie.jpg') no-repeat;
  }
}
</style>
  