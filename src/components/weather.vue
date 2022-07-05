<template>
  <main>
    <aside>
      <form @submit.prevent="getData()" v-if="weather">
        <h3 class="fas fa-search"></h3>
        <input type="text" placeholder="Search" v-model="city" />
        <h3 class="fas fa-location-dot"></h3>
      </form>
      <div class="icon" v-if="weather">
        <img :src="icon" alt="" />
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
        <h2>WHETHERSA</h2>
        <ul>
          <li>°C</li>
          <li>°F</li>
          <li>Moon</li>
        </ul>
      </nav>
      <ul class="days">
        <li v-for="i in 5" :key="i">
          <h3>Tue</h3>
          <img src="../assets/animated/cloudy-day-1.svg" alt="" />
          <h3>12°C</h3>
        </li>
      </ul>
      <div class="options">
        <h3>Today's Highlights</h3>
        <ul>
          <li>
            <p>UV Index</p>
            <img src="https://weather.baronsa.dev/uv.png" alt="" />
          </li>
          <li>
            <p>Wind Staus</p>
            <h2>7.70km/h</h2>
          </li>
          <li>
            <p>Sunrise & Sunset</p>
            <span>
              <img src="" alt="" />
              <p>6:30am</p>
            </span>
            <span>
              <img src="" alt="" />
              <p>6:30am</p>
            </span>
          </li>
          <li>
            <p>Humidity</p>
            <h2>70%</h2>
          </li>
          <li>
            <p>Visibility</p>
            <h2>5.2 km</h2>
          </li>
          <li>
            <p>Pressure</p>
            <h2>1013.25 hPa</h2>
          </li>
        </ul>
      </div>
    </article>
  </main>
</template>
<script>
import cloudy1 from "../assets/animated/cloudy-day-1.svg";
import sunny from "../assets/animated/day.svg";

export default {
  data() {
    return {
      icon: "",
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

          let text = data.current.condition.text;
          if (text == "Sunny") {
            this.icon = sunny;
          } else if (text == "Partly cloudy") {
            this.icon = cloudy1;
          }
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
  },
};
</script>
