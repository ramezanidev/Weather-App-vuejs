<template>
  <div class="table">
    <div class="thead">
        <span>Date</span>
        <span>Description</span>
        <span>Temp</span>
        <span>Weather</span>
    </div>
    <div class="tbody">
        <div v-for="Data in dataTable" :key="Data">
            <span>{{ Data.dt_txt.slice(5, 16) }}</span>
            <span>{{ Data.weather[0].description }}</span>
            <span>{{ Math.floor(Data.main.temp_min - 273) + "° / " + Math.floor(Data.main.temp_max - 273)+"°"}}</span>
            <span>
                <img :src="`http://openweathermap.org/img/wn/${Data.weather[0].icon}@2x.png`">
            </span>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    props:["dataTable"],
}
</script>

<style scoped>
.table{
    width: 100%;
    height: 100%;
    position: relative;
    padding-top: 50px
}
.thead span:first-child {
    width: 30%;
    justify-content: flex-start;
}
.thead span {
    height: 100%;
    align-items: center;
    display: flex;
    padding: 5px;
    flex: auto;
    width: 23.3%;
    justify-content: center;
}
.thead{
    width: 100%;
    box-shadow: 0 20px 18px -17px rgb(0 0 0 / 32%);
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid hsla(0,0%,81.2%,.8666666666666667);
    color: #fff;
    font-family: Vazir;
    line-height: 18px;
    font-size: 17px;
    position: absolute;
    top: 0;
    left: 0;
}
.tbody{
    height: 100%;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    display: flex;
    flex-direction: column;
    overflow: hidden auto;
    scroll-behavior: smooth;
    scrollbar-color: #06f hsla(0,0%,100%,0);
    scrollbar-width: thin;
}
.tbody::-webkit-scrollbar{
    width: 3px;
    background-color: hsla(0,0%,100%,0);
}
.tbody::-webkit-scrollbar-thumb{
    background-color: #06f;
}
.tbody div{
    width: 100%;
    height: 45px;
    transition: all .2s ease-in-out;
    cursor: pointer;
    border-bottom: 1px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #fff;
    font-family: Vazir;
    font-size: 14px;
}
.tbody div span:first-child{
    width: 30%;
    justify-content: flex-start
}
.tbody div span{
    height: 100%;
    display: flex;
    width: 23.3%;
    flex: auto;
    align-items: center;
    justify-content: center;
    padding: 5px;
}
span img {
    width: 60px;
}
</style>