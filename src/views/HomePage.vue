<template>
  <div class="home-page">
    <h1 ref="title"></h1>
  </div>
  <div class="homepage">
    <Weather />
  </div>
</template>

<script>
import Weather from '../components/WeatherWidget.vue';

export default {
  name: 'HomePage',
  components: {
    Weather,
  },
}
</script>

<style>
.homepage {
  text-align: center;
}

.home-page h1 {
  font-size: 2em;
  margin: 20px;
  font-family: 'Courier New', Courier, monospace;
  white-space: pre; 
  text-align: center;
}
</style>
