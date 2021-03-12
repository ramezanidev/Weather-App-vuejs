<template>
  <div class="snowflakes" :class="{ 'snowflake-day': isDay }">
    <div class="clouds-snow"></div>
  </div>
</template>

<script>
import { SnowflakeJs } from "@aicdev/snowflakejs";
export default {
  name: "Snow",
  props: {
    isDay: Boolean
  },
  mounted() {
    const snowflake = new SnowflakeJs(500, 250, 5000, 6, 15);
    snowflake.init();
  }
};
</script>

<style>
.snowflakes {
  width: 100%;
  height: 100%;
  background-color: #000;
}
.snowflake-day {
  background: linear-gradient(
    to top,
    #0114cd 0,
    #000983 27%,
    #005cb8 100%
  ) !important;
}
.clouds-snow {
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
</style>
