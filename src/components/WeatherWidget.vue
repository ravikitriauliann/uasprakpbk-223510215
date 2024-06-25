<template>
  <div class="weather-widget">
    <h2>CUACA KOTA ANDA</h2>
    <div class="search-bar">
      <input v-model="city" placeholder="Enter city name" @keyup.enter="getWeather" />
      <button @click="getWeather">Search</button>
    </div>
    <div v-if="weather" class="weather-info">
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Location:</strong> {{ weather.name }}</p>
        <img src="../assets/loc.png" alt="location icon" />
        <div class="weather-border"></div>
      </div>
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Temperature:</strong> {{ weather.main.temp }}°C</p>
        <img src="../assets/temp.png" alt="temperature icon" />
        <div class="weather-border"></div>
      </div>
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Weather:</strong> {{ weather.weather[0].description }} </p>
        <img :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}.png`" alt="weather icon" />
        <div class="weather-border"></div>
      </div>
    </div>
    <div v-else>
      <p>Masukkan nama kota untuk melihat kondisi cuaca dikota anda.</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const city = ref('')
const weather = ref(null)

const getWeather = async () => {
  const apiKey = '8a7436bc7a340da337b17310ea4fd29a'
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=${apiKey}`

  try {
    const response = await axios.get(url)
    weather.value = response.data
  } catch (error) {
    console.error(error)
    weather.value = null
  }
}
</script>

<style scoped>
.weather-widget {
  padding: 20px;
  border: 1px solid var(--medium-red);
  border-radius: 10px;
  max-width: 700px;
  margin: 100px auto 50px auto;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5); /* Warna latar belakang agak gelap */
  backdrop-filter: blur(5px); /* Efek blur pada latar belakang */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); /* Bayangan agak gelap */
}

.weather-widget h2 {
  color: white; /* Warna teks menjadi putih */
  font-size: 36px;
  font-weight: bold;
  margin-bottom: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.search-bar input {
  padding: 10px;
  width: 60%;
  margin-right: 10px;
  border: 1px solid var(--medium-red);
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.1); /* Warna latar belakang input agak gelap */
  color: white; /* Warna teks input menjadi putih */
  transition: box-shadow 0.3s ease-in-out;
}

.search-bar input:focus {
  box-shadow: 0 0 5px var(--medium-red);
}

.search-bar button {
  padding: 10px;
  border: 1px solid var(--dark-red);
  background-color: var(--medium-red);
  color: var(--light-beige);
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.search-bar button:hover {
  background-color: var(--dark-red);
}

.search-bar button:active {
  transform: scale(0.95);
}

.weather-info {
  margin-top: 40px;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.weather-item {
  margin: 20px;
  border: 1px solid var(--medium-red);
  border-radius: 5px;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.1); /* Warna latar belakang item agak gelap */
  color: white; /* Warna teks item menjadi putih */
  text-align: center;
  width: 220px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  animation: backgroundColorChange 3s ease infinite;
}

.weather-item img {
  margin-top: 10px;
  width: 35px;
  height: 35px;
}

.weather-item p {
  margin: 0;
  color: white; /* Mengubah warna teks deskripsi menjadi putih */
  font-weight: bold;
}

.weather-border {
  border-top: 1px solid var(--medium-red);
  margin-top: 10px;
  padding-top: 10px;
}

.animate-item {
  animation: fadeIn 2s ease-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(-10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes backgroundColorChange {
  0% {
    background-color: rgba(255, 255, 255, 0.1); /* Warna latar belakang awal */
  }
  50% {
    background-color: rgba(255, 255, 255, 0.3); /* Warna latar belakang perubahan */
  }
  100% {
    background-color: rgba(255, 255, 255, 0.1); /* Warna latar belakang kembali */
  }
}
</style>
