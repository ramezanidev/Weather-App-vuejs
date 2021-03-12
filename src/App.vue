<template>
  <Panel />
</template>

<script>
import Panel from "./components/panel";
export default {
  name: "App",
  components: {
    Panel
  }
};
</script>

<style>
@import url("https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.css");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}
html,
body {
  width: 100%;
  height: 100%;
}
</style>
