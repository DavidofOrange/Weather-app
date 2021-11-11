<template>
  <div id="card" :class="typeof weather.main != 'undefined' && weather.main.temp > 25 ? 'warm' : '' || typeof weather.main != 'undefined' && weather.main.temp < 1 ? 'cold' : ''">
    <main> 
      <Title />
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search by city..." 
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div> 
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°</div>
          <div class="weather-condition">{{ weather.weather[0].main }}</div> 
        </div>
        <div class="date">{{ dateBuilder() }}</div> 
      </div>
    </main>

  </div>
</template>

<script>
import Title from './Title.vue';

export default {
  name: 'Weather',
  components: {
    Title
  },
  
  
  data () {
    return {
      api_key: '87fb07099eaa8e6b663227638add6eb3',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      showTitle: true,
    }
  },
  methods: {
    fetchWeather (e) {
      if(e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    }, 
    setResults (results) {
      this.weather = results;
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
    

      return  `${month} ${date}, ${year}`;
    }
  }
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@500;700;900&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Red Hat Display', sans-serif;
    max-height: 100%;
  }

  #card {
    position: absolute;
    display: flex;
    justify-content: center;
    padding: 20px;
    width: 90%;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    overflow: hidden;
    border-radius: 20px;
    box-shadow: -5px 10px 100px hsl(226, 22%, 73%);
    margin: 20px 0;
    font-family: 'Red Hat Display', sans-serif;
    background-image: url('../assets/cool.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  #card.warm {
    background-image: url('../assets/warm_desktop.jpg');
  }

   #card.cold {
    background-image: url('../assets/cold_desktop.jpg');
  }

  main { 
    min-height: 100vh;
    padding: 20px;
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0,0,0, 0.75));
    width: 100%;
    height: 100%;
    border-radius: 20px;
  }

  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    border:none;
    outline: none;
    background: none;
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }

  .search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 16px 0px 16px 0px;
  }

  .location-box .location {
    color: #FFF;
    font-size: 34px;
    font-weight: 600;
    text-align: center;
    text-shadow: 2px 3px rgba(0, 0, 0, 0.55);
    font-style: italic;
  }

  .date {
    padding-top: 20px;
    color: #FFF;
    font-size: 25px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
    text-shadow: 3px 6px 5px rgba(0, 0, 0, 0.25);
  }

  .weather-box {
    text-align: center;
  }

  .weather-box .temp {
    display: inline-block;
    padding: 10px 25px;
    color: #FFF;
    font-size: 5rem;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    margin: 20px 0;
    box-shadow: 3px 6px 3px rgba(0, 0, 0, 0.25);
  }

  .weather-box, .weather-condition {
    color: #FFF;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

   @media only screen and (max-width: 600px) {
    .weather-box .temp {
      font-size: 3rem;
    }
    .location-box .location {
      font-size: 24px;
      font-weight: 400;
    }
    .weather-box, .weather-condition {
      color: #FFF;
      font-size: 30px;
      font-weight: 700;
      font-style: italic;
      text-shadow: 2px 4px rgba(0, 0, 0, 0.25);
    }
    .date {
      padding-top: 15px;
      font-size: 20px;
      text-shadow: 2px 4px rgba(0, 0, 0, 0.25);
    }
  }
   @media only screen and (max-width: 325px) {
    #card {
      display: flex;
      justify-content: center;
    }
    .weather-box .temp {
      font-size: 1.6rem;
      font-weight: 700;
      text-shadow: 2px 3px rgba(0, 0, 0, 0.25);
  }
    .weather-box .weather-condition {
      color: #FFF;
      font-size: 25px;
      font-weight: 700;
      font-style: italic;
      text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    }
   .date {
    padding-top: 10px;
    font-size: 15px;
  }
  }
</style>
