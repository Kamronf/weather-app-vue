<template>
<div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp < 16? 'warm' : '' ">
  <main>

    <div class="search-box">
      <h2>Ob-havo ma'lumoti
      </h2>
      <h4>Shaharni kiriting</h4>
      <input type="text" class="search-bar" placeholder="search " v-model="query" @keypress="fetchWeather"/>

    </div>

<div class="wether-wrap" v-if="typeof weather.main != 'undefined'" >
  <div class="location-box">
    <div class="location"> {{ weather.name }}, {{weather.sys.country}}</div>
    <div class="data">{{ dateBuilder() }}</div>
  </div>
  <div class="weather-box">
    <div class="temp">{{Math.round(weather.main.temp)}} °C</div>
    <div class="weather">{{weather.weather[0].main}}</div>
  </div>
</div>

  </main>
</div>
</template>

<script>
export default {
name: 'app',
data() {
  return {
    api_key: '5f6cfcacf7ecccd8f9f677bbf8227680',
    url_base: 'https://api.openweathermap.org/data/2.5/' , 
    query: ' ',
    weather: {}
  }
},
methods: {
  fetchWeather(e){
    if(e.key=="Enter"){
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(res =>{
        return res.json();
      }).then(this.setResults)
    }

  },
  setResults(results){
    this.weather = results;
  },
  dateBuilder(){
    let d = new Date()
    let months = ["Yanvar" , "Fevral","Mart","Aprel","May","Iyun","Iyul","Avgust","Sentabr","Oktabr","Noyabr","Dekabr"];
    let days = ["Yakshanba" ,"Dushanba", "Seshanba","Chorshanba", "Payshanba","Juma","Shanba"];

    let day = days[d.getDay()]
    let date = d.getDate()
    let month = months[d.getMonth()]
    let year = d.getFullYear()

    return`${day} ${date} ${month} ${year}`
  }
},
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}
body{
  font-family: montserrat , sans-serif;
}
#app{
    background-image: url(./assets/summer.jpg);
    background-size: cover;
    background-position: center;
    transition: .4s;
}
#app.warm{
  background-image: url('./assets/winter.jpg');

}
main{
  display: grid;
  grid-template-columns: 50% 50%;
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom , rgba(242, 245, 248, 0.024),rgba(0,0,0,6));
}
.search-box{
  width:90%;
}
.search-box h2{
    color: #ffff;
  margin-top: 20vh;
  font-size: 50px;
  font-style: italic;
  text-align: left;
  font-weight: 500;
}
.search-box h4{
    color: #ffff;
    margin-top: 7vh;
  font-size: 20px;
  font-style: italic;
  text-align: left;
  font-weight: 500;
}
.search-box .search-bar{
  display: block;
  margin-top: 2vh;
  width: 100%;
  padding: 15px;
  color: #3d3434;
  font-size: 20px;
  border: none;
  background: none;
  outline: none;
  appearance: none;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, .25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  transition: .4s;
}
.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, .75);
  border-radius: 16px 0px 16px 0px;

}
.location-box .location{
  color: #ffff;
  margin-top: 10vh;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.location-box .data{
  color: #ffff;
  margin-top: 1vh;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box{
text-align: center;
margin-top: 3vh;

}
.weather-box .temp{
  display: inline-block;
  margin-top: 3vh;
  padding: 10px 25px;
  color: #ffff;
  font-size: 100px;
  font-weight: 900;
  text-shadow: 3px 6px  rgba(0, 0, 0, .25);
  background-color:  rgba(0, 0, 0, .25);
  border-radius: 16px 16px 16px 16px;
  box-shadow: rgba(0, 0, 0, .25);
}
.weather-box .weather{
  margin-top: 5vh;
  color: #ffff;
  font-size: 28px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, .25);
}
</style>