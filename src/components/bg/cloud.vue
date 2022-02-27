<template>
  <div :class="{ 'cloud-cover': props.isDay }">
    <div v-if="props.isDay" class="clouds-cloud"></div>

    <div v-if="!props.isDay" class="stars"></div>
    <div v-if="!props.isDay" class="twinkling"></div>
    <div v-if="!props.isDay" class="clouds"></div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  isDay: {
    type: Boolean,
  },
});
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
  background: #000 url('~/public/img/stars.png') repeat top center;
  z-index: 0;
}

.twinkling {
  background: transparent url('~/public/img/twinkling.png') repeat top center;
  z-index: 1;

  -moz-animation: move-twink-back 200s linear infinite;
  -ms-animation: move-twink-back 200s linear infinite;
  -o-animation: move-twink-back 200s linear infinite;
  -webkit-animation: move-twink-back 200s linear infinite;
  animation: move-twink-back 200s linear infinite;
}

.clouds {
  background: transparent url(~/public/img/clouds2.png) repeat top center;
  z-index: 3;
  -moz-animation: move-clouds-back 700s linear infinite;
  -ms-animation: move-clouds-back 700s linear infinite;
  -o-animation: move-clouds-back 700s linear infinite;
  -webkit-animation: move-clouds-back 700s linear infinite;
  animation: move-clouds-back 700s linear infinite;
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
.cloud-cover {
  width: 100%;
  height: 100%;
  filter: brightness(0.7);
  background: linear-gradient(to top, #0216d9 0, #010daa 27%, #0070df 100%);
}
.clouds-cloud {
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 3;
  width: 100%;
  height: 100%;
  display: block;
  position: absolute;
  filter: invert(0.9);
  background-size: contain;
  background-position: center;
  background-color: transparent;
  background-image: url(~/public/img/clouds2.png);
  animation: move-clouds-back 700s linear infinite;
  animation: move-clouds-back 700s linear infinite;
  -o-animation: move-clouds-back 700s linear infinite;
  -ms-animation: move-clouds-back 700s linear infinite;
  -moz-animation: move-clouds-back 700s linear infinite;
  -webkit-animation: move-clouds-back 700s linear infinite;
}
@media (max-width: 768px) {
  .clouds-cloud {
    background-size: cover;
  }
}
</style>
