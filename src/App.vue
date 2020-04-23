<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : 'storm'">
    <main>
      <img src="./assets/weather-logo.png"><br>
<!--      <h1>Weather App</h1><br>-->
      <div class="search-box">
        <input type="text" class="search-bar"
               placeholder="Search...."
               v-model="query"
               @keypress="fetchWeather">
      </div>

      <div class="weather-wrap" v-if="typeof  weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}},{{ weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>
      </div>

      <div class="weather-box"  v-if="typeof  weather.main != 'undefined'">
        <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
        <div class="weather">{{weather.weather[0].main}}</div>

<!--      Here is the details of the weather of particular area we have entered in the search box-->

        <div >
          <table id="weather">
          <tr>
            <td>Wind</td>
            <td>{{weather.wind.speed }}m/s,({{weather.wind.deg}})</td>
          </tr>
          <tr>
            <td>Humidity</td>
            <td>{{weather.main.humidity}} %</td>
          </tr>
          <tr>
            <td>Pressure</td>
            <td>{{weather.main.pressure}}</td>
          </tr>
          <tr>
            <td>Latitude</td>
            <td>{{weather.coord.lat}}</td>
          </tr>
          <tr>
            <td>Longitude</td>
            <td>{{weather.coord.lon}}</td>
          </tr>

        </table>
        </div>
      </div>

    </main>
  </div>
</template>
<script>
export default {
  name:"app",
  data() {
    return {
      api_key:'8ed240b208982c104af0fd5b1819fc4d',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
    fetchWeather(e){
     if(e.key == "Enter"){
        //fetch is the javascript library to for making requests just like axios
        fetch( `${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    },
      dateBuilder(){
          let d = new Date();
          let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
          let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

          let day = days[d.getDay()];
          let date = d.getDate();
          let month = months[d.getMonth()];
          let year = d.getFullYear();
          return `${day} ${date} ${month} ${year}`;
      }
}


}
</script>

<style>
* {
  margin:0;
  padding:0;
  box-sizing: border-box;
}
h1{
    text-align: center;
  color: whitesmoke;
 }
  body{
    font-family: 'montserrat', sans-serif;
  }
  #app{
    background-image: url("./assets/sky-bg.jpg");
    background-size:cover;
    background-position: bottom;
    transition: 0.4s;
  }
  #app.warm{
    background-image: url("./assets/hot-bg.jpg");
  }
  #app.storm{
  background-image: url("./assets/storm-clouds-bg.jpg");

  }
  main{
    /*vh vertical height which will bring our pic to our screen size*/
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.25));
  }
  search-box{
    width: 100%;
    margin-bottom: 30px;
  }
.search-box .search-bar {
  display: block;
  width:100%;
  padding: 15px;

  color:#313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color:rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
  .search-box .search-bar:focus{
    box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.75);
    border-radius: 16px 0px 16px 0px ;
  }

  .location-box .location{
    color:whitesmoke;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,0.25);
  }
  .location-box .date{
    color:whitesmoke;
    font-size: 20px;
    font-weight: 300;
    font-style:italic;
    text-align: center;
  }
  .weather-box{
    text-align: center;
  }
  .weather-box .temp{
    display: inline-block;
    padding: 10px 25px;
    color: whitesmoke;
    font-size: 102px;
    font-weight: 900;

    text-shadow:3px 6px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.25);
    border-radius: 16px;
    margin :30px 2px;

    box-shadow: 3px 6px rgba(0,0,0,0.25 );
  }
  .weather-box .weather{
    color: whitesmoke;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow:3px 6px rgba(0,0,0,0.25 );
  }
#weather {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#weather td, #weather th {
  border: 1px solid #ddd;
  padding: 8px;
}

#weather tr:nth-child(even){background-color: #f2f2f2;}

#weather th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: grey;
  color: white;
}
.right {
  position: absolute;
  right: 0px;
  width: 200px;
  border: 3px solid #white;
  padding: 10px;
}
img{
  alignment: left;
  height: 50px;
  width: 50px;
}
</style>
