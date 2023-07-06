<template>
  <div class="weather-widget">
    <h2>Weather Widget</h2>
    <div class="location-container">
      <button @click="getLocation">Get Current Location</button>
      <p>Latitude: {{ latitude }}</p>
      <p>Longitude: {{ longitude }}</p>
      <p v-if="country">Country: {{ country }}</p>
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
      latitude: null,
      longitude: null,
      country: null,
      weatherData: null,
    };
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.showPosition);
      } else {
        console.error('Geolocation is not supported by this browser.');
      }
    },
    showPosition(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
      this.getCountry();
      this.getWeatherData();
    },
    async getCountry() {
      try {
        const apiUrl = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${this.latitude}&longitude=${this.longitude}&localityLanguage=en`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        if (data.countryName) {
          this.country = data.countryName;
        }
      } catch (error) {
        console.error(error);
      }
    },
    async getWeatherData() {
      try {
        const apiKey = 'YOUR_API_KEY';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?lat=${this.latitude}&lon=${this.longitude}&appid=${apiKey}`;

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

.location-container {
  margin-top: 20px;
}

.location-container button {
  padding: 8px 16px;
  margin-bottom: 10px;
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
