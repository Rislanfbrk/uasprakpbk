<template>
  <div class="weather-widget">
    <h2 class="widget-title">Weather Widget</h2>
    <div class="location-input">
      <label for="location">Enter Location:</label>
      <br>
      <br>
      <input type="text" id="location" v-model="location" />
      <br>
      <br>
      <button @click="fetchWeatherData">Get Weather</button>
    </div>
    <div v-if="weatherData" class="weather-data">
      <p class="location">Location: {{ weatherData.name }}</p>
      <p v-if="weatherData.main" class="temperature">
        Temperature: {{ weatherData.main.temp }}°C
      </p>
      <p v-if="weatherData.weather" class="description">
        Description: {{ weatherData.weather[0].description }}
      </p>
    </div>
    <p v-else>Loading weather data...</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: '',
      weatherData: null
    };
  },
  methods: {
    async fetchWeatherData() {
      try {
        const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        this.weatherData = data;
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    }
  }
};
</script>

<style scoped>
.weather-widget {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
}

.widget-title {
  margin-top: 0;
  color: #333;
}

.location-input {
  margin-bottom: 10px;
}

.location-input input#location {
  padding: 10px;
  font-size: 20px;
  transform: scale(1.0);
  border: 1px solid #ccc;
  border-radius: 4px;
}

.weather-data {
  margin-top: 10px;
}

.location {
  font-size: 18px;
  font-weight: bold;
}

.temperature {
  font-size: 24px;
  color: #ff5722;
}

.description {
  font-size: 16px;
}
</style>
