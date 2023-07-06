<template>
  <div class="weather-widget">
    <h2>Weather Widget</h2>
    <div class="input-container">
      <input type="text" v-model="location" placeholder="Enter location" />
      <button @click="getWeatherData">Get Weather</button>
    </div>
    <div v-if="weatherData" class="weather-info">
      <div class="weather-icon">
        <img :src="weatherData.icon" :alt="weatherData.description" />
      </div>
      <div class="weather-description">
        <p>{{ weatherData.description }}</p>
        <p>Temperature: {{ weatherData.temperature }}°C</p>
        <p>Humidity: {{ weatherData.humidity }}%</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      location: '',
      weatherData: null,
    };
  },
  methods: {
    async getWeatherData() {
      try {
        const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        this.weatherData = {
          icon: `http://openweathermap.org/img/w/${data.weather[0].icon}.png`,
          description: data.weather[0].description,
          temperature: Math.round(data.main.temp - 273.15),
          humidity: data.main.humidity,
        };
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style scoped>
.weather-widget {
  text-align: center;
}

.input-container {
  margin-top: 20px;
}

.input-container input {
  padding: 8px;
  margin-right: 10px;
}

.weather-info {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.weather-icon img {
  width: 100px;
  height: 100px;
}

.weather-description {
  margin-left: 20px;
}
</style>
