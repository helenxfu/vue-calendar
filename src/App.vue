<template>
  <div id="app">
    <h1>Vue Calendar</h1>
    <Calendar/>
    <p class="credit">&#169; Starcloud</p>
  </div>
</template>

<script>
import Calendar from "./components/Calendar";

export default {
  name: "app",
  components: {
    Calendar
  }
};
</script>

<style>
#app {
  font-family: "Cookie", cursive, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(64, 75, 71);
}
* {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background-color: rgb(233, 219, 208);
  font-size: 16px;
}
a {
  text-decoration: none;
  color: rgb(184, 48, 116);
  cursor: pointer;
  transition-duration: 0.4s;
}
img {
  width: 100%;
}
.noselect {
  -webkit-touch-callout: none;
  /* iOS Safari */
  -webkit-user-select: none;
  /* Safari */
  -khtml-user-select: none;
  /* Konqueror HTML */
  -moz-user-select: none;
  /* Firefox */
  -ms-user-select: none;
  /* Internet Explorer/Edge */
  user-select: none;
  /* Non-prefixed version, currently supported by Chrome and Opera */
}
input,
select,
button {
  border: none;
  outline: none;
  font-size: 12px;
  cursor: pointer;
  font-family: "Cookie", cursive, sans-serif;
}
select {
  margin: 0 3px;
}
button {
  text-decoration: none;
  padding: 5px;
  border-radius: 15px;
  transition-duration: 0.3s;
}
h1 {
  font-size: 30px;
  margin: 30px 0 15px;
}
.credit {
  margin-top: 20px;
}
</style>
