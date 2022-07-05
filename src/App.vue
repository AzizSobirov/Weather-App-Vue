<template>
  <div class="app">
    <weather></weather>
    <!-- <div :class="app_search">
      <div class="input">
        <input
          type="search"
          placeholder="Search City or Town"
          id="as_input"
          v-model="input"
        />
        <button id="as_btn" @click="fetchWeather()">
          <a href="#">Search</a>
        </button>
      </div>
      <p>{{ error }}</p>
    </div>
    <div class="app_content">
      <h3>{{ city }}</h3>
      <img :src="img" :alt="city" />
      <h2>{{ temp }}°C</h2>
      <p>{{ description }}</p>
      <ul>
        <li>
          <h4>Sunrise Time - {{ sunrise }}</h4>
        </li>
        <li>
          <h4>Sunset Time - {{ sunset }}</h4>
        </li>
        <li>
          <a href="https://sobirov.netlify.app">Created By Aziz Sobirov</a>
        </li>
      </ul>
    </div> -->
  </div>
</template>

<script>
import "@/assets/css/style.css";
import weather from "@/components/weather.vue";
export default {
  name: "app",
  data() {
    return {
      city: "",
      img: "",
      temp: "",
      description: "",
      input: "",
      app_search: "app_search",
      error: "",
      sunrise: "",
      sunset: "",
    };
  },
  components: {
    weather,
  },
  methods: {
    fetchWeather() {
      fetch(
        "https://api.openweathermap.org/data/2.5/weather?q=" +
          this.input +
          "&appid=eaeeace2fb4d17b1a46b8328d8b961a4"
      )
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          if (data.cod == "404") {
            this.error = "City Not Found";
          } else {
            this.app_search += "-hide";
          }
          this.city = data.name;
          this.temp = Math.floor(data.main.temp - 273.15);
          this.img = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
          this.description = data.weather[0].description;
          // sunrise
          let unix_time = data.sys.sunrise;
          var date = new Date(unix_time * 1000);
          var hours = date.getHours();
          var minutes = "0" + date.getMinutes();
          this.sunrise = hours + ":" + minutes.substr(-2);
          // sunset
          let unix_time2 = data.sys.sunset;
          var date2 = new Date(unix_time2 * 1000);
          var hours2 = date2.getHours();
          var minutes2 = "0" + date2.getMinutes();
          this.sunset = hours2 + ":" + minutes2.substr(-2);
        });
    },
  },
};
</script>
