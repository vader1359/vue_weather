
<template>
  <div class="container">
    <div class="grid-item date">
      <div>{{Date(current_weather.dt*1000)}}</div>
      <div></div>
    </div>
    <div class="grid-item location">
      {{current_weather.name}}
    </div>
    <div class="grid-item temperature">{{Math.round(current_weather.main.temp).toFixed(1)}}</div>
    <div class="grid-item description">
      {{current_weather.weather[0].description}}
    </div>
    <div class="grid-item image">
      <img class="weather-img" src="../assets/images/weather.svg" alt="">
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  name: "Weather",
  data() {
    return {
      current_weather: null
    };
  },

  mounted() {
    axios
      .get(
        "https://api.openweathermap.org/data/2.5/find?q=Stockholm&units=metric&appid=dfe15a41201d660911d013203832e676"
      )
      .then(response => {
        this.current_weather = response.data.list[0];
      });
  }
};

const formattedDateTime = unixTime => {
  if (unixTime) {
    return moment.unix(unixTime).format("MM/DD/YYYY");
  } else {
    ("Today");
  }
};
</script>
