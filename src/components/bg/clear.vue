<template>
  <div :class="{ 'clear-cover': isDay }">
    <div v-if="isDay" class="clouds-clear"></div>

    <div v-if="!isDay" class="stars"></div>
    <div v-if="!isDay" class="twinkling"></div>
    <div v-if="!isDay" class="clouds"></div>
  </div>
</template>

<script>
export default {
  name: "clear",
  props: ["isDay"]
};
</script>

<style>
@keyframes move-twink-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -10000px 5000px;
  }
}
@-webkit-keyframes move-twink-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -10000px 5000px;
  }
}
@-moz-keyframes move-twink-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -10000px 5000px;
  }
}
@-ms-keyframes move-twink-back {
  from {
    background-position: 0 0;
  }
  to {
    background-position: -10000px 5000px;
  }
}

.stars,
.twinkling,
.clouds {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  display: block;
}

.stars {
  background: #000 url(/img/stars.png) repeat top center;
  z-index: 0;
}

.twinkling {
  background: transparent url(/img/twinkling.png) repeat top center;
  z-index: 1;

  -moz-animation: move-twink-back 200s linear infinite;
  -ms-animation: move-twink-back 200s linear infinite;
  -o-animation: move-twink-back 200s linear infinite;
  -webkit-animation: move-twink-back 200s linear infinite;
  animation: move-twink-back 200s linear infinite;
}

.clouds {
  background: transparent url(/img/clouds.png) repeat top center;
  z-index: 3;

  -moz-animation: move-clouds-back 200s linear infinite;
  -ms-animation: move-clouds-back 200s linear infinite;
  -o-animation: move-clouds-back 200s linear infinite;
  -webkit-animation: move-clouds-back 200s linear infinite;
  animation: move-clouds-back 200s linear infinite;
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
.clear-cover {
  width: 100%;
  height: 100%;
  background: linear-gradient(to top, #0216d9 0, #010daa 27%, #0070df 100%);
}
.clouds-clear {
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 3;
  width: 100%;
  height: 100%;
  display: block;
  height: 300px;
  position: absolute;
  background-size: contain;
  background-position: center;
  background-color: transparent;
  background-image: url(/img/clouds.png);
  animation: move-clouds-back 700s linear infinite;
  animation: move-clouds-back 700s linear infinite;
  -o-animation: move-clouds-back 700s linear infinite;
  -ms-animation: move-clouds-back 700s linear infinite;
  -moz-animation: move-clouds-back 700s linear infinite;
  -webkit-animation: move-clouds-back 700s linear infinite;
}
</style>
