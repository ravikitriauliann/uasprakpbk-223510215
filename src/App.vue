<template>
  <q-layout view="hHh lpR fFf">
    <!-- Header -->
    <q-header elevated class="custom-header">
      <q-toolbar class="custom-toolbar" style="background-color: darkolivegreen;">
        <div class="toolbar-left">
          <q-btn-dropdown class="custom-dropdown" label="TUGAS" dropdown-icon="#">
            <q-list class="nav-list">
              <q-item clickable v-close-popup>
                <router-link to="/">
                  <q-item-section>
                    <q-item-label class="nav-label">Weather</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas1">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 1</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas2">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 2</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas3">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 3</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas4">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 4</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas5">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 5</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
              <q-item clickable v-close-popup>
                <router-link to="/tugas6">
                  <q-item-section>
                    <q-item-label class="nav-label">TUGAS 6</q-item-label>
                  </q-item-section>
                </router-link>
              </q-item>
            </q-list>
          </q-btn-dropdown>
        </div>
        <div class="toolbar-spacer"></div>

        <!-- Display Time and Date -->
        <div class="time-display">
          <p class="time">{{ formattedTime }}</p>
          <p class="date">{{ formattedDate }}</p>
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view></router-view>
    </q-page-container>

    <!-- Full-screen background video -->
    <video id="background-video" loop autoplay muted>
      <source src="./assets/first-fall-day-in-forest.1920x1080.mp4" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </q-layout>
</template>

<script>
import { ref, onMounted, onUnmounted, computed } from 'vue'

export default {
  name: 'App',
  setup() {
    const currentTime = ref(new Date())

    // Function to update the time every second
    const updateTime = () => {
      currentTime.value = new Date()
    }

    // Start and stop the interval for updating the time
    onMounted(() => {
      const interval = setInterval(updateTime, 1000)
      onUnmounted(() => clearInterval(interval))
    })

    // Computed properties for formatted time and date
    const formattedTime = computed(() => {
      return currentTime.value.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    })

    const formattedDate = computed(() => {
      return currentTime.value.toLocaleDateString([], { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })
    })

    return {
      formattedTime,
      formattedDate
    }
  }
}
</script>

<style>
@import './assets/index.css';

/* Header and Toolbar */
.custom-toolbar {
  color: var(--light-beige);
  text-decoration: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.toolbar-left {
  display: flex;
  align-items: center;
}

.toolbar-spacer {
  flex: 1;
}

/* Time and Date Display Styling */
.time-display {
  text-align: right;
  color: white;
  font-weight: bold;
  margin-right: 20px;
}

.time {
  font-size: 24px;
}

.date {
  font-size: 16px;
}

/* Dropdown and Navigation */
.custom-dropdown {
  background-color: var(--medium-red);
  color: var(--light-beige);
}

.nav-list {
  background-color: var(--dark-red);
  color: var(--light-beige);
}

.q-item-section {
  color: var(--beige) !important;
}

.nav-label {
  font-weight: bold;
  color: black !important;
}

.nav-link {
  margin: 0 20px;
  color: var(--light-beige);
  text-decoration: none;
  font-weight: bold;
  transition: color 0.3s, transform 0.3s;
}

.nav-link:hover {
  color: var(--beige);
  transform: scale(1.1);
}

.nav-link:active {
  transform: scale(0.9);
}

/* General Body Styling */
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  background: white; /* Set a simple background color */
}

.q-layout, .q-page-container {
  background: transparent; /* Ensure the layout and page container backgrounds are transparent */
}

/* Full-screen background video */
#background-video {
  position: fixed;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
  z-index: -1; /* Send the video to the background */
  background: no-repeat;
  background-size: cover;
}

/* Adjusting for Responsive Design */
@media (max-width: 600px) {
  .nav-link {
    margin: 0 10px;
  }
}
</style>
