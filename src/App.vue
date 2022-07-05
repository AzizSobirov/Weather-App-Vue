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

  components: {
    weather,
  },
};
</script>
