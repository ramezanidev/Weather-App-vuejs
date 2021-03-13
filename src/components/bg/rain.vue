<template>
  <div class="bg back-row-toggle splat-toggle" :class="{ 'rain-day': isDay }">
    <div class="clouds-rain"></div>
    <div class="rain front-row" v-html="rain1"></div>
    <div class="rain back-row" v-html="rain2"></div>
  </div>
</template>

<script>
export default {
  name: "rain",
  props: ["isDay"],
  data() {
    return {
      rain2: "",
      rain1: ""
    };
  },
  mounted() {
    var increment = 0;
    var drops = "";
    var backDrops = "";
    while (increment < 100) {
      var randoHundo = Math.floor(Math.random() * (98 - 1 + 1) + 1);
      var randoFiver = Math.floor(Math.random() * (5 - 2 + 1) + 2);
      increment += randoFiver;
      drops += `<div class="drop" style="left:calc(${increment}% + 300px); bottom:${randoFiver +
        randoFiver -
        1 +
        100}%; animation-delay: 0.${randoHundo}s; animation-duration: 0.5${randoHundo}s;"><div class="stem" style="animation-delay: 0.${randoHundo}s; animation-duration: 0.5 ${randoHundo}s;"></div><div class="splat" style="animation-delay: 0.${randoHundo}s; animation-duration: 0.5${randoHundo}s;"></div></div>`;
      backDrops += `<div class="drop" style="right:${increment}%; bottom: ${randoFiver +
        randoFiver -
        1 +
        100}%; animation-delay: 0.${randoHundo}s; animation-duration: 0.5${randoHundo}s;"><div class="stem" style="animation-delay: 0.${randoHundo}s; animation-duration: 0.5${randoHundo}s;"></div><div class="splat" style="animation-delay: 0.${randoHundo}s; animation-duration: 0.5${randoHundo}s;"></div></div>`;
    }
    this.rain1 = drops;
    this.rain2 = backDrops;
  }
};
</script>

<style>
.bg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin: 0;
  overflow: hidden;
  background: linear-gradient(to bottom, #010012 0, #020024 83%, #000630 100%);
}
.rain-day {
  background: linear-gradient(
    to top,
    #0216d9 0,
    #010daa 27%,
    #0070df 100%
  ) !important;
}
.clouds-rain {
  background: transparent url(/img/clouds2.png) repeat top center;
  z-index: 3;
  width: 100%;
  height: 600px;
  opacity: 0.6;
  z-index: 10;
  background-size: contain;
  background-repeat: repeat;
  animation: move-clouds-back 500s linear infinite;
  position: absolute;
  top: -250px;
}

@keyframes move-clouds-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: 10000px 0;
  }
}
@-webkit-keyframes move-clouds-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: 10000px 0;
  }
}
@-moz-keyframes move-clouds-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: 10000px 0;
  }
}
@-ms-keyframes move-clouds-back {
  from {
    background-position: 0;
  }
  to {
    background-position: 10000px 0;
  }
}

.rain {
  position: absolute;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
}

.rain.back-row {
  display: none;
  z-index: 1;
  bottom: 60px;
  opacity: 0.5;
}

.back-row-toggle .rain.back-row {
  display: block;
}

.drop {
  position: absolute;
  bottom: 100%;
  width: 15px;
  height: 120px;
  pointer-events: none;
  animation: drop 0.5s linear infinite;
}

@keyframes drop {
  0% {
    transform: translate(0px, 0vh) rotate(25deg);
  }

  75% {
    transform: translate(-300px, 90vh) rotate(22deg);
  }

  100% {
    transform: translate(-300px, 90vh) rotate(16deg);
  }
}

.stem {
  width: 1px;
  height: 60%;
  margin-left: 7px;
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.096),
    rgba(255, 255, 255, 0.267)
  );
  animation: stem 0.5s linear infinite;
}

@keyframes stem {
  0% {
    opacity: 1;
  }

  65% {
    opacity: 1;
  }

  75% {
    opacity: 0;
  }

  100% {
    opacity: 0;
  }
}

.splat {
  width: 15px;
  height: 10px;
  border-top: 2px dotted rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  opacity: 1;
  transform: scale(0);
  animation: splat 0.5s linear infinite;
  display: none;
}

.splat-toggle .splat {
  display: block;
}

@keyframes splat {
  0% {
    opacity: 1;
    transform: scale(0);
  }

  80% {
    opacity: 1;
    transform: scale(0);
  }

  90% {
    opacity: 0.5;
    transform: scale(1);
  }

  100% {
    opacity: 0;
    transform: scale(1.5);
  }
}

.toggles {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 3;
}

.toggle {
  position: absolute;
  left: 20px;
  width: 50px;
  height: 50px;
  line-height: 51px;
  box-sizing: border-box;
  text-align: center;
  font-family: sans-serif;
  font-size: 10px;
  font-weight: bold;
  background-color: rgba(255, 255, 255, 0.2);
  color: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  cursor: pointer;
  transition: background-color 0.3s;
}

.toggle:hover {
  background-color: rgba(255, 255, 255, 0.25);
}

.toggle:active {
  background-color: rgba(255, 255, 255, 0.3);
}

.toggle.active {
  background-color: rgba(255, 255, 255, 0.4);
}

.back-row-toggle {
  line-height: 12px;
  padding-top: 14px;
}

.single-toggle {
  top: 160px;
}

.single-toggle .drop {
  display: none;
}

.single-toggle .drop:nth-child(10) {
  display: block;
}
</style>
