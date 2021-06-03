<template>
  <input
    type="text"
    id="formInput"
    v-model="input"
    required
    @keypress="fetchWeather"
    placeholder="   Search here..."
    ref="input"
  />

  <div class="error-msg">
    <!-- <h1 class="error-msg">{{ this.errorMsg }}</h1> -->
  </div>
  <div class="weather-content" v-if="showData">
    <div class="search-info">
      <h1 class="place krona" v-if="showData">
        {{ this.weather.name }}, {{ this.weather.sys.country }}
      </h1>

      <small class="date"><i>Sunday 12 January, 2020</i></small>
    </div>
    <div class="temp">
      <h1>{{ this.weather.main.temp.toFixed(0) }}°c</h1>
    </div>
    <h1 class="weather-info krona">
      {{ this.weather.weather[0].description }}
    </h1>
  </div>
  <!-- <button @click="getLocation">start</button> -->
</template>
<script>
export default {
  name: "searchForm",
  emits: ['bgClass'],
  data() {
    return {
      apiKey: "e7d61398e3b4124ab4f7bd68bffaf97c",
      baseUrl: "https://api.openweathermap.org/data/2.5/weather?",
      weather: {
        location : {
          name : '',
          region: ''
        },
        current: {
          temperature: '',
          weather_descriptions: ['']
        }
      },
      input: "",
      showData: false,
      weatherTerms: [
        "rain",
        "shower",
        "rainy",
        "sunny",
        "clear",
        "haze",
        "fog",
        "cloudy",
        "clouds",
        "snow",
        "thunder",
        "overcast",
        "mist",
        "foggy",
        "storm",
        "sky"
      ],
      bgClass: "",
      errorMsg: "",
    };
  },
  mounted() {
    this.getLocation();
    this.$refs.input.focus();
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        //check if geolocation is available
       

        navigator.geolocation.getCurrentPosition(this.autoWeather);
        
      }
    },

    autoWeather(position) {
      
      fetch(
        `${this.baseUrl}lat=${position.coords.latitude}&lon=${position.coords.longitude}&units=metric&appid=${this.apiKey}`
      )
        .then((res) => res.json())
        .then(this.setResults);
        
    },
    fetchWeather(e) {
      if (e.keyCode == 13) {
       
        fetch(`${this.baseUrl}&q=${this.input}&units=metric&appid=${this.apiKey}`)
          .then((res) => {
            // if (res.status == 200) {
           
            return res.json();
            // }
          })
          .then(this.setResults)
          .catch((error) => this.showErrorMsg);
          
      }
    },

    setResults(result) {
      if (result) {
        
        this.weather = result;
        this.showData = true;
        // document.querySelector(".error-msg").innerHTML = "";
        this.input = "";
        this.setBg();
        console.log(this.weather.weather[0].description.toLowerCase());
      }
    },

    setBg() {
      let currentDesc = this.weather.weather[0].description.toLowerCase();
      
      this.weatherTerms.forEach((term) => {
        currentDesc.indexOf(term) >= 0 ? (this.bgClass = term) : "";

        this.$emit("bgClass", this.bgClass);
      });
    },
    showErrorMsg(err) {
      this.showData = false;
      this.errorMsg = "Please Allow Location to Autodetect.";
    },
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Caveat+Brush&display=swap");
* {
  margin: 0;
  padding: 0;
}
.krona {
  /* font-family: 'Caveat Brush', cursive; */
}

.temp,
#formInput {
  background: rgba(255, 255, 255, 0.15);
  box-shadow: 0 8px 32px 0 rgba(255, 255, 255, 0.17);
  backdrop-filter: blur(9px);
  -webkit-backdrop-filter: blur(6px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  display: inline-block;
}
#formInput {
  min-width: 300px;
  width: 50%;
  border: none;
  outline: none;
  font-size: 2rem;
  text-align: center;
  color: white;
  padding: 0.5rem 0;
  font-family: cursive;
  border-radius: 0px;
  border-top-left-radius: 10px;
  border-bottom-right-radius: 10px;
  margin-bottom: 3rem;
}
#formInput::placeholder {
  color: rgba(255, 255, 255, 0.55);
}
.place {
  padding: 0.5rem;
}
.search-info {
  margin-bottom: 3rem;
}
.temp h1 {
  margin: 0;
  font-size: 5.5rem;
  padding: 1.5rem 2rem;
}
.weather-info {
  margin-top: 1.5rem;
  font-size: 2rem;
}
.error {
  text-align: center;
}


/* Change the white to any color */
input:-webkit-autofill,
input:-webkit-autofill:hover, 
input:-webkit-autofill:focus, 
input:-webkit-autofill:active
{
 transition: background-color 5000s;
-webkit-text-fill-color: #fff !important;
}

</style>
