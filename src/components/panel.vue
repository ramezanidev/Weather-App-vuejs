<template>
  <div id="section" class="container">
    <transition name="laoding">
      <div v-if="isLoading" class="loading-page">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          width="197px"
          height="197px"
          viewBox="0 0 100 100"
          preserveAspectRatio="xMidYMid"
        >
          <circle
            cx="50"
            cy="50"
            r="25"
            stroke-width="2"
            stroke="#ff0000"
            stroke-dasharray="39.269908169872416 39.269908169872416"
            fill="none"
            stroke-linecap="round"
          >
            <animateTransform
              attributeName="transform"
              type="rotate"
              dur="1.7384615384615383s"
              repeatCount="indefinite"
              keyTimes="0;1"
              values="0 50 50;360 50 50"
            ></animateTransform>
          </circle>
          <circle
            cx="50"
            cy="50"
            r="22"
            stroke-width="2"
            stroke="#0053f1"
            stroke-dasharray="34.55751918948772 34.55751918948772"
            stroke-dashoffset="34.55751918948772"
            fill="none"
            stroke-linecap="round"
          >
            <animateTransform
              attributeName="transform"
              type="rotate"
              dur="1.7384615384615383s"
              repeatCount="indefinite"
              keyTimes="0;1"
              values="0 50 50;-360 50 50"
            ></animateTransform>
          </circle>
        </svg>
      </div>
    </transition>
    <div class="bg">
      <component :isDay="isDay" :is="bgComponent" />
    </div>
    <Weather
      class="Weather"
      @loading-start="isLoading = true"
      @loading-end="isLoading = false"
      @isDay="isDayChange"
      @status-weather="(e) => (status = e)"
    />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

import Weather from "./weather/weather-app";

import Rain from "./bg/rain";
import Clear from "./bg/clear";
import Snow from "./bg/snow";
import Cloud from "./bg/cloud";

const isLoading = ref(false);
const isDay = ref(false);
const status = ref(null);

const isDayChange = (payload) => {
  isDay.value = payload;
};

const bgComponent = computed(() => {
  switch (status.value) {
    case "Thunderstorm":
    case "Drizzle":
    case "Rain": {
      return Rain;
    }
    case "Snow": {
      return Snow;
    }
    case "Clear":
    case "Haze": {
      return Clear;
    }
    case "Clouds": {
      return Cloud;
    }
    default: {
      return "div";
    }
  }
});
</script>

<style scoped lang="scss">
.container {
  width: 100%;
  height: 100%;
  position: relative;
}
.bg {
  overflow: hidden;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.loading-page {
  position: fixed;
  z-index: 100;
  width: 100%;
  height: 100%;
  display: flex;
  backdrop-filter: blur(2px) brightness(0.8);
  svg {
    margin: auto;
    display: block;
  }
}

.laoding-enter-active,
.laoding-leave-active {
  transition: 0.7s;
}
.laoding-enter-from,
.laoding-leave-to {
  opacity: 0;
}
.Weather {
  position: fixed;
  width: calc(100% - 50px);
  height: calc(100% - 50px);
  z-index: 10;
  background-color: #ffffff05;
  margin: 25px;
  box-shadow: 0px 0px 19px 0px #0003;
  border: 1px solid #ffffff17;
  border-radius: 5px;
  backdrop-filter: blur(1px);
  padding: 10px;
  display: flex;
}
@media (max-width: 768px) {
  .Weather {
    width: 100%;
    margin: 0;
    height: 100%;
    overflow: scroll;
    display: block;
  }
}
</style>
