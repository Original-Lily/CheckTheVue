<template>
  <header>
    <h3>Weather APP - created by Original-Lily</h3>
    <p>Using: VueJS, OpenAPI & OpenWeatherMapAPI</p>
  </header>
  <div class="app-container">
    <div class="left-panel">
      <h1>Vue Weather App</h1>
      <input v-model="city" placeholder="Enter city" @keyup.enter="getWeather" />
      <button @click="getWeather">Get Weather</button>
      <div v-if="weatherData">
        <h2>{{ weatherData.name }}, {{ weatherData.sys.country }}</h2>
        <p>{{ weatherData.weather[0].description }}</p>
        <p>Temperature: {{ weatherData.main.temp }}°C</p>
        <p>Feels like: {{ weatherData.main.feels_like }}°C</p>
      </div>
    </div>
    <div class="right-panel" :style="{ backgroundImage: `url('${backgroundImage}')` }">
      <div v-if="generatedImage">
        <img :src="generatedImage" alt="Generated Image" />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import OpenAI from 'openai';

const openai = new OpenAI({ apiKey: '' });
const openweathermapApiKey = '';

export default {
  data() {
    return {
      city: '',
      weatherData: null,
      generatedImage: null,
    };
  },
  computed: {
    backgroundImage() {
      return this.generatedImage || 'https://via.placeholder.com/1200x800';
    },
  },
  methods: {
    async getWeather() {
      try {
        const weatherResponse = await axios.get('https://api.openweathermap.org/data/2.5/weather', {
          params: {
            q: this.city,
            appid: openweathermapApiKey,
            units: 'metric',
          },
        });
        this.weatherData = weatherResponse.data;
        const prompt = `Photograph of the skyline and the Weather in ${this.city}: ${this.weatherData.weather[0].description}, Temperature: ${this.weatherData.main.temp}°C`;
        const imageResponse = await openai.images.generate({ prompt });
        console.log('Weather response:', weatherResponse.data);
        console.log('Image response:', imageResponse);
        this.generatedImage = imageResponse.data[0].url;
      } catch (error) { console.error('Error:', error); }
    },
  },
};

</script>

<style scoped>
body {
  margin: 0;
  overflow: hidden;
}

header {
  text-align: center;
}

.app-container {
  display: flex;
  height: 100vh;
}

.left-panel {
  flex: 1;
  background-color: rgb(235, 235, 235);
  padding: 20px;
  color: rgb(0, 0, 0);
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.right-panel {
  flex: 1;
  background-color: rgb(215, 215, 215);
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.weather-background {
  width: 50%;
  max-height: 70vh;
  overflow: hidden;
}

.weather-background img {
  width: 100%;
  height: auto;
  max-width: 100%;
}

h1, p, input, button {
  margin-bottom: 10px;
}
</style>
