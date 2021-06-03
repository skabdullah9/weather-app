<template>
  <div class="wrapper" :class="[this.class]">
    <div class="container">
      <searchForm @bgClass="this.setClass" />
      
    </div>
  </div>
</template>

<script>
import searchForm from "./components/searchForm.vue";

export default {
  name: "App",
  components: {
    searchForm,
  },
  data() {
    return {
      class: ''
    }
  },
  methods: {
    setClass(gif) {
      this.class = gif;
      
    },
  },
};
</script>

<style>

body {
  font-family: cursive;
  margin: 0;
  overflow: hidden;
}
.wrapper {
  background-color: #333;
  color: #fff;
  height: 100vh;
}
.wrapper.cloudy,
.wrapper.overcast,
.wrapper.clouds {
  background:linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/cloudy.gif) no-repeat;
}
.wrapper.haze {
   background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/haze.gif) no-repeat;
}
.wrapper.sunny,
.wrapper.clear {
    background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/sunny.gif) no-repeat;
}
.wrapper.rain,
.wrapper.rainy,
.wrapper.shower {
   background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/rain.gif) no-repeat;
}
.wrapper.mist,
.wrapper.foggy {
  background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/fog.gif) no-repeat;
}
.wrapper.thunder,
.wrapper.storm {
  background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/thunder.gif) no-repeat;
}
.wrapper.sky {
  background: linear-gradient(45deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(./assets/sun.gif) no-repeat;
}

.wrapper.haze,
.wrapper.cloudy,
.wrapper.clouds,
.wrapper.sunny,
.wrapper.clear,
.wrapper.rain,
.wrapper.rainy,
.wrapper.shower,
.wrapper.overcast,
.wrapper.mist,
.wrapper.foggy,
.wrapper.thunder,
.wrapper.storm,
.wrapper.sky  {
  background-size: cover;
  background-position: center;
  height: 100vh;
  max-height: 100%;
}

.container {
  max-width: 1140px;
  width: 95%;
  margin: 0 auto;
  box-sizing: border-box;
  text-align: center;
  padding-top: 5rem;
}
</style>
