<template>
  <div>
    <div class="temp-box">
      <div class="temp">
        <div>
          <h2>{{ Math.floor(data.main.temp) - 273 }}<span>C</span></h2>
          <p>
            {{ Math.floor(data.main.temp_min) - 273 }}&#xb0;c |
            {{ Math.floor(data.main.temp_max) - 273 }}&#xb0;c
          </p>
          <b>{{ data.weather[0].description }}</b>
        </div>
      </div>
      <div class="location">
        <b>{{ data.name }}</b>
        <span>Latest update: {{ updateDate }}</span>
      </div>
      <div class="tool-bar">
        <button class="refresh" @click="loadData"></button>
        <button class="location"></button>
      </div>
      <div class="details">
        <svg width="80" height="80" title="Humidity">
          <circle
            r="35"
            cx="40"
            cy="40"
            style="
              stroke: #a8a8a84d;
              stroke-width: 4px;
              backdrop-filter: inherit;
              fill: #ffffff21;
            "
          ></circle>
          <circle
            stroke="white"
            stroke-width="4"
            style="transform: rotate(272deg); transform-origin: center"
            fill="transparent"
            r="35"
            cx="40"
            cy="40"
            ref="circle"
          />
          <text
            x="26"
            y="45"
            style="font-family: 'Vazir'; fill: #fff; font-weight: bold"
          >
            {{ data.main.humidity }}%
          </text>
        </svg>
        <div>
          <span>
            <span>visibility:</span>
            <span>{{ data.visibility }}m</span>
          </span>
          <span>
            <span>pressure:</span>
            <span>{{ data.main.pressure }}</span>
          </span>
          <span>
            <span>timezone:</span>
            <span>{{ timezone }}</span>
          </span>
        </div>
      </div>

      <div class="wind">
        <div class="turbines">
          <div class="turbine">
            <div class="pilot">
              <div class="prop-container">
                <div class="prop"></div>
                <div class="prop"></div>
                <div class="prop"></div>
              </div>
            </div>
            <div class="pole"></div>
          </div>
          <div class="turbine turbine2">
            <div class="pilot">
              <div class="prop-container">
                <div class="prop"></div>
                <div class="prop"></div>
                <div class="prop"></div>
              </div>
            </div>
            <div class="pole"></div>
          </div>
        </div>
        <div class="wind-table">
          <span>
            <span>Speed:</span>
            <span>{{ data.wind.speed || 0  }}Km/h</span>
          </span>
          <span>
            <span>deg:</span>
            <span>{{ data.wind.deg || 0  }}&#xb0;</span>
          </span>
          <span style="border-bottom: none">
            <span>gust:</span>
            <span>{{ data.wind.gust || 0 }}Km/h</span>
          </span>
          <div>
            <div class="compass">
              <span>N</span>
              <div
                class="compass-inline"
                :style="{
                  transform: `translate(-50%, -50%) rotate(${data.wind.deg}deg)`,
                }"
              >
                <div></div>
                <div></div>
              </div>
            </div>
            <img
              :src="`http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`"
            />
          </div>
        </div>
      </div>
      <div class="Skycondition">
        <div class="Circle" ref="Skycondition">
          <img class="sun" src="/img/icon/sun.svg" />
        </div>
      </div>
      <div class="sunTime">
        <div>
          <span>{{
            sunset.getHours().toString().padStart(2, "0") +
            ":" +
            sunset.getMinutes().toString().padStart(2, "0")
          }}</span>
          <span>{{
            sunrise.getHours().toString().padStart(2, "0") +
            ":" +
            sunrise.getMinutes().toString().padStart(2, "0")
          }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  computed: {
    sunset: function () {
      return new Date(
        this.data.sys.sunset * 1000 +
          new Date().getTimezoneOffset() * 60000 +
          this.data.timezone * 1000
      );
    },
    sunrise: function () {
      return new Date(
        this.data.sys.sunrise * 1000 +
          new Date().getTimezoneOffset() * 60000 +
          this.data.timezone * 1000
      );
    },
    isDay: function () {
      let now = new Date();
      let utc_timestamp = new Date(
        now.getUTCFullYear(),
        now.getUTCMonth(),
        now.getUTCDate(),
        now.getUTCHours(),
        now.getUTCMinutes(),
        now.getUTCSeconds(),
        now.getUTCMilliseconds()
      );
      let TimeZone = new Date(
        utc_timestamp.getTime() + this.data.timezone * 1000
      );
      let a = new Date(
        this.data.sys.sunset * 1000 +
          new Date().getTimezoneOffset() * 60000 +
          this.data.timezone * 1000
      ).getTime();
      let b = TimeZone.getTime();
      console.log(TimeZone);
      return a > b;
    },
    updateDate: function () {
      let time = new Date(this.data.dt * 1000);
      return (
        time.getHours().toString().padStart(2, "0") +
        ":" +
        time.getMinutes().toString().padStart(2, "0")
      );
    },
    timezone: function () {
      return (
        Math.floor(this.data.timezone / 3600)
          .toString()
          .padStart(2, "0") +
        ":" +
        ((this.data.timezone % 3600) / 60).toString().padStart(2, "0")
      );
    },
    weather: function () {
      const weather = ["clear"];
      let status;
      let w = this.data.weather[0].description.toLowerCase();
      for (let i = 0; i < weather.length; i++) {
        if (w.includes(weather[i])) {
          status = weather[i];
          break;
        }
      }
      return status;
    },
  },
  data() {
    return {
      token: "49f01e8b459085de2580f891869cdbe4",
      city: "khoy",
      data: {
        clouds: { all: 19 },
        dt: 1615215600,
        dt_txt: "2021-03-08 15:00:00",
        main: {
          feels_like: 278.53,
          grnd_level: 881,
          humidity: 10,
          pressure: 1009,
          sea_level: 1009,
          temp: 281.99,
          temp_kf: 1.27,
          temp_max: 281.99,
          temp_min: 28000.72,
        },
        pop: 0.28,
        pod: "n",
        sys: { sunset: 10 },
        visibility: 10000,
        weather: [
          { id: 801, main: "Clouds", description: "few clouds", icon: "02n" },
        ],
        0: { id: 801, main: "Clouds", description: "few clouds", icon: "02n" },
        wind: { speed: 2.11, deg: 255 },
      },
    };
  },
  methods: {
    setProgress: function () {
      const circle = this.$refs.circle;
      const radius = circle.r.baseVal.value;
      const circumference = radius * 2 * Math.PI;
      const offset =
        circumference - (this.data.main.humidity / 100) * circumference;
      circle.style.strokeDasharray = `${circumference} ${circumference}`;
      circle.style.strokeDashoffset = `${circumference}`;
      circle.style.strokeDashoffset = offset;

      if (!this.isDay) {
        this.$refs.Skycondition.style.transform =
          "translate(-50%, 0) rotate(180deg)";
      } else {
        let now = new Date();
        let utc_timestamp = new Date(
          now.getUTCFullYear(),
          now.getUTCMonth(),
          now.getUTCDate(),
          now.getUTCHours(),
          now.getUTCMinutes(),
          now.getUTCSeconds(),
          now.getUTCMilliseconds()
        );
        let TimeZone = new Date(
          utc_timestamp.getTime() + this.data.timezone * 1000
        );
        let a =
          new Date(
            this.data.sys.sunset * 1000 +
              new Date().getTimezoneOffset() * 60000 +
              this.data.timezone * 1000
          ).getTime() -
          new Date(
            this.data.sys.sunrise * 1000 +
              new Date().getTimezoneOffset() * 60000 +
              this.data.timezone * 1000
          ).getTime();
        let b =
          TimeZone.getTime() -
          new Date(
            this.data.sys.sunrise * 1000 +
              new Date().getTimezoneOffset() * 60000 +
              this.data.timezone * 1000
          ).getTime();

        let c = (b / a) * 100;
        let d = (c * 180) / 100;
        this.$refs.Skycondition.style.transform = `translate(-50%, 0) rotate(${-d}deg)`;
      }
    },
    loadData: function () {
      this.$emit("loading-start");
      fetch(
        `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.token}`
      )
        .then((response) => response.json())
        .then((data) => {
          this.data = data;
          console.log(this.data);
          this.$emit("isDay", this.isDay);
          this.$emit("loading-end");
          this.$emit("status-weather", this.data.weather[0].main);
          this.setProgress();
        });
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style lang="scss">
.temp-box {
  font-family: "Vazir";
  width: 270px;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.temp {
  width: 100%;
  height: 220px;
  display: flex;
  color: #fff;
  div {
    margin: auto;
    h2 {
      font-size: 64px;
      line-height: 54px;
      text-align: center;
      span {
        font-size: 30px;
      }
    }
    p {
      text-align: center;
      font-size: 13px;
      word-spacing: -2px;
      line-height: 15px;
      color: #ccc;
    }
    b {
      text-align: center;
      width: 100%;
      display: block;
      font-size: 15px;
      line-height: 23px;
      color: #ccc;
    }
    b::first-letter {
      text-transform: uppercase;
    }
  }
}
.location {
  width: 100%;
  border-bottom: 1px solid #a8a8a8;
  height: 36px;
  display: flex;
  color: #e1e1e1;
  text-align: center;
  justify-content: space-between;
  flex-direction: row-reverse;
  padding: 5px;
  align-items: flex-end;
  padding: 5px 5px 3px;
  b {
    font-size: 24px;
    line-height: 22px;
  }
  span {
    font-size: 12px;
  }
}
.tool-bar {
  display: flex;
  justify-content: space-between;
  padding: 5px;
  button {
    -webkit-mask-size: 100% 100%;
    background-color: rgb(233, 233, 233);
    border: none;
    width: 18px;
    cursor: pointer;
    transition: 0.2s all ease-in-out;
    outline: none;
    height: 18px;
  }
  button:hover {
    background-color: rgb(145, 145, 145);
  }
  button.refresh {
    -webkit-mask-image: url(/img/icon/refresh.svg);
  }
  button.location {
    -webkit-mask-image: url(/img/icon/location.svg);
  }
}
.details {
  display: flex;
  justify-content: space-between;
  padding: 4px;
  > svg {
    margin-right: 25px;
    min-width: 80px;
  }
  > div {
    display: flex;
    flex-wrap: wrap;
    flex: auto;
    > span:last-child {
      border: none;
    }
    > span {
      display: flex;
      text-transform: capitalize;
      justify-content: space-between;
      width: 100%;
      font-family: "Vazir";
      color: rgb(211, 211, 211);
      border-bottom: 1px solid #ffffff61;
      font-size: 14px;
      height: 26px;
      font-weight: lighter;
      span:last-child {
        color: #fff;
        font-weight: bold;
      }
    }
  }
}

.wind-table span:last-child {
  border-bottom: none !important;
  border: none !important;
}
.wind-table {
  display: flex;
  flex-direction: column;
  flex: auto;
  div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    img {
      width: 56px;
      height: 56px;
      border-radius: 50%;
      border: 1px solid #646477;
    }
  }
  > span {
    display: flex;
    text-transform: capitalize;
    justify-content: space-between;
    width: 100%;
    font-family: "Vazir";
    color: rgb(211, 211, 211);
    border-bottom: 1px solid #ffffff61;
    font-size: 14px;
    height: 26px;
    font-weight: lighter;
    span:last-child {
      color: #fff;
      font-weight: bold;
    }
  }
}
@media (max-width: 768px) {
  .temp-box {
    width: 100%;
  }
}
.wind {
  display: flex;
  margin-top: 5px;
  padding: 4px;
  width: 100%;
  height: 150px;
  .turbines {
    height: 100%;
    display: flex;
    min-width: 90px;
    width: 90px;
    position: relative;
    margin-right: 15px;
  }
}
.turbines {
  .turbine {
    width: 90px;
    position: relative;
    height: 100%;
    border-bottom: 2px double #b8b8b8;
    .pilot {
      position: absolute;
      width: 14px;
      height: 14px;
      border: 1px solid #ffffff;
      background-color: #555555;
      border-radius: 50%;
      top: 44px;
      left: 38px;
      z-index: 2;
      transform-style: preserve-3d;
    }
    .prop-container {
      width: 80px;
      height: 80px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) translateZ(-10px);
      position: absolute;
      z-index: unset;
      animation: 2s turbines infinite linear;
      .prop {
        background-color: white;
        width: 7px;
        height: 40px;
        border-radius: 40%;
        position: absolute;
      }
      .prop:nth-child(1) {
        top: 0;
        left: 50%;
        transform: translate(-50%, 0);
      }
      .prop:nth-child(2) {
        bottom: 0;
        left: 0;
        transform: translate(4px, -13px) rotate(50deg);
        transform-origin: bottom;
      }
      .prop:nth-child(3) {
        bottom: 0;
        right: 0;
        transform: translate(-4px, -13px) rotate(-50deg);
        transform-origin: bottom;
      }
    }
    .pole {
      width: 4px;
      height: 100px;
      bottom: 0;
      position: absolute;
      background-color: #727272;
      left: 50%;
      transform: translate(-50%, 0);
      border-radius: 2px;
    }
  }
}
.turbine2 {
  position: absolute !important;
  right: 0;
  bottom: 0;
  transform: translate(25px, 20px) scale(0.7);
  filter: brightness(0.7) blur(1px);
  border-bottom: none !important;
}
@keyframes turbines {
  to {
    transform: translate(-50%, -50%) translateZ(-10px) rotate(356deg);
  }
}
.compass {
  height: 56px;
  width: 56px;
  margin-top: 8px;
  border-radius: 50%;
  position: relative;
  border: 1px solid #646477;
  .compass-inline {
    position: absolute;
    top: 50%;
    left: 50%;
    transform-origin: center;
    height: 50px;
    width: 8px;
    transform: translate(-50%, -50%);
    div:nth-child(1) {
      width: 1px;
      height: 50px;
      border-left: 4px solid transparent;
      border-right: 4px solid transparent;
      border-bottom: 20px solid #ef5052;
      position: absolute;
      top: 0%;
      transform: translate(0, -50%);
    }
    div:nth-child(2) {
      border-left: 4px solid transparent;
      border-right: 4px solid transparent;
      border-top: 20px solid #f3f3f3;
      width: 1px;
      position: absolute;
      top: 100%;
      transform: translate(0, -50%);
      height: 50px;
    }
  }
  span {
    color: black;
    background-color: white;
    z-index: 1;
    font-family: "Vazir";
    font-weight: bold;
    font-size: 11px;
    overflow: hidden;
    text-align: center;
    height: 14px;
    width: 14px;
    border-radius: 50%;
    line-height: 11px;
    display: flex;
    vertical-align: middle;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

.Skycondition {
  width: 100%;
  box-shadow: inset 0px -11px 20px -18px #000;
  overflow: hidden;
  height: 120px;
  border-bottom: 1px solid #e8e8e8;
  position: relative;
  .Circle {
    width: 200px;
    position: absolute;
    border: 1px dashed #dddddd;
    height: 200px;
    border-radius: 50%;
    left: 50%;
    top: 20px;
    transform: translate(-50%, 0) rotate(-29deg);
    .sun {
      position: absolute;
      width: 20px;
      height: 20px;
      top: 50%;
      right: 0;
      transform: translate(+50%, -50%);
    }
  }
}
.sunTime {
  display: flex;
  height: 30px;
  padding: 3px 0;
  color: #fff;
  font-family: "Vazir";
  font-size: 13px;
  user-select: none;
  div {
    width: 200px;
    margin: auto;
    position: relative;
    height: 100%;
    span {
      position: absolute;
      top: 0;
    }
    span:nth-child(1) {
      left: 0;
      transform: translate(-50%, 0);
    }
    span:nth-child(2) {
      right: 0;
      transform: translate(50%, 0);
    }
  }
}
</style>
