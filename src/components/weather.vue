<template>
  <main>
    <aside>
      <form @submit.prevent="getData()" v-if="weather">
        <h3 class="fas fa-search"></h3>
        <input type="text" placeholder="Search" v-model="city" />
        <h3 class="fas fa-location-dot"></h3>
      </form>
      <div class="icon" v-if="weather">
        <img :src="getIcon(weather.current.condition.code)" alt="" />
        <h1>{{ weather.current.temp_c }}°C</h1>
      </div>
      <div class="text" v-if="weather">
        <h3>{{ weather.location.name }}</h3>
        <p>{{ getTime() }}</p>
        <hr />
        <span>
          <i class="fas fa-cloud"></i>
          <p>{{ weather.current.condition.text }}</p>
        </span>
        <span>
          <i class="far fa-clock"></i>
          <p>{{ weather.current.last_updated }}</p>
        </span>
      </div>
    </aside>
    <article>
      <nav>
        <h2>Weather</h2>
        <ul>
          <li class="active">°C</li>
          <li>°F</li>
          <li><h2 class="fas fa-moon"></h2></li>
        </ul>
      </nav>
      <ul class="days" v-if="weather">
        <li v-for="i in weather.forecast.forecastday" :key="i.id">
          <h3>{{ getDay(i.date) }}</h3>
          <img :src="getIcon(i.day.condition.code)" alt="" />
          <h3>{{ i.day.avgtemp_c }}°C</h3>
        </li>
      </ul>
      <div class="options" v-if="weather">
        <h3>Today's Highlights</h3>
        <ul>
          <li>
            <p>UV Index</p>
            <img src="https://weather.baronsa.dev/uv.png" alt="" />
          </li>
          <li>
            <p>Wind Staus</p>
            <h2>{{ weather.current.wind_kph }}kph</h2>
            <img
              src="https://cdn-icons-png.flaticon.com/512/959/959711.png"
              style="width: 50px;"
              alt=""
            />
          </li>
          <li>
            <p>Sunrise & Sunset</p>
            <span>
              <img src="../assets/animated/1000.svg" alt="" />
              <p>{{ weather.forecast.forecastday[0].astro.sunrise }}</p>
            </span>
            <span>
              <img src="../assets/animated/night.svg" alt="" />
              <p>{{ weather.forecast.forecastday[0].astro.sunset }}</p>
            </span>
          </li>
          <li>
            <p>Humidity</p>
            <h2>{{ weather.current.humidity }}%</h2>
          </li>
          <li>
            <p>Visibility</p>
            <h2>{{ weather.current.vis_km }}km</h2>
          </li>
          <li>
            <p>Pressure</p>
            <h2>{{ weather.current.pressure_mb }}hPa</h2>
          </li>
        </ul>
      </div>
    </article>
  </main>
</template>
<script>
// import cloudy1 from "../assets/animated/";
// import sunny from "../assets/animated/day.svg";

export default {
  data() {
    return {
      city: "London",
      weather: null,
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      fetch(
        "https://api.weatherapi.com/v1/forecast.json?key=56ba6428a62242f6b0a113745220507&q=" +
          this.city +
          "&days=7&aqi=no&alerts=no"
      )
        .then((res) => res.json())
        .then((data) => {
          this.weather = data;
          console.log(data);
        });
    },
    getTime() {
      let date = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[date.getDay()];
      let today = date.getDate();
      let month = months[date.getMonth()];
      //   let year = date.getFullYear();
      return day + ", " + month + " " + today;
    },
    getDay(val) {
      let d = new Date(val);
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      return days[d.getDay()];
    },
    getIcon(val) {
      return require("../assets/animated/" + val + ".svg");
    },
  },
};
</script>
