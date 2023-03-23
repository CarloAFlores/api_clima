<template>
<div id="app">
  <main>
    <div class="search-box">
      <input type="text" 
      class="search-bar" 
      placeholder="Buscando..."
      v-model="query"
      v-on:keypress="fetchWeather"
      />
    </div>

    <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
      <div class="location-box">
        <div class="location">{{weather.name}}, {{ weather.sys.country }}</div>
        <div class="date">{{dateBuilder()}}</div>
      </div>

    <div class="weather-box">
      <div class="temp">{{ Math.round(weather.main.temp)}}</div>
      <div class="weather">{{weather.weather[0].main}}</div>
    </div>  

    </div>
  </main>
</div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
    api_key: `72b433bf737a1adb736fa23e2024ab9e`,
    url_base:"https://api.openweathermap.org/data/2.5/",
    query: '',
    weather:{}
  }
  },
  methods:{
    fetchWeather(e){
      if(e.key == "Enter"){
        console.log(this.query);
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res =>{
          return res.json();
        }).then(this.setResults);

      }
    },
    setResults(results){
      this.weather = results;
      console.log(results)
    },
    dateBuilder(){
      let d = new Date()
      let months =["Enero","Febrero","Marzo","Abril",
      "Mayo","Junio","Julio","Agosto","Septiembre","Octubre",
      "Noviembre","Diciembre",];
      let days = ["Lunes","Martes","Miercoles",
      "Jueves","Viernes","Sabado","Domingo",];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;

}
body{
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

#app{
  background-image: radial-gradient(circle at 23.7% 106.41%, #ffb757 0, #ffbc4c 5%, #ffbf41 10%, #efc237 15%, #ddc42f 20%, #c9c527 25%, #b3c523 30%, #9bc421 35%, #7fc324 40%, #5ec02a 45%, #2bbc32 50%, #00b83c 55%, #00b348 60%, #00af56 65%, #00ab66 70%, #00a876 75%, #00a588 80%, #00a29a 85%, #009fad 90%, #009dbf 95%, #009cd2 100%);
}

main{
  min-height: 100vh;
  padding: 25px;
}

.search-box{
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;

  color:  #131311;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 0px rgba(255, 255, 255, 0.25);
  background-color:rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(255, 255, 255, 0.25);
  background-color:rgba(255, 255, 255, 0.75);
  border-radius: 16px 0 px 16px 0px;
}

.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: 500px;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, .25);
}
.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.weather-box .weather{
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

</style>
