<script>
import axios, { Axios } from "axios";
export default {
  data() {
    return { city: "", error: "", info: null };
  },
  computed: {
    cityName() {
      return "<<" + this.city + ">>";
    },
    showTemp() {
      return "Temperature NOW : " + this.info.main.temp;
    },
    showFeelsLike() {
      return "Feels Like : " + this.info.main.feels_like;
    },
    showMinTemp() {
      return "Minimal Temperature : " + this.info.main.temp_min;
    },
    showMaxTemp() {
      return "Maximium Temperature : " + this.info.main.temp_max;
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = alert(
          "ERROR!  Write name of the city more than 2 letters"
        );
        return false;
      }

      this.error = "";

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=1f0a447e37781df1d4c898814da66680`
        )
        .then((res) => (this.info = res.data));
    }
  }
};
</script>
<template>
  <div className="wrapper">
    <h2>The weather App</h2>
    <p>
      Find out the weather in
      {{ city == "" ? "YOUR CITY" : cityName }}
    </p>
    <input type="text" v-model="city" placeholder="Enter city" />
    <button v-if="city != ''" @click="getWeather()">Get the weather</button>
    <button disabled v-else="city != ''">Enter name of city</button>
    <div className="Natija" v-if="info != null">
      <p>{{ showTemp }}%</p>
      <p>{{ showFeelsLike }}%</p>
      <p>{{ showMinTemp }}%</p>
      <p>{{ showMaxTemp }}%</p>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 100%;
  height: 500px;
  border-radius: 50px;
  background-color: #1f0f24;
  padding: 5px;
  text-align: center;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  @media only screen and (min-width: 600px) {
    width: 600px;
  }
}

.wrapper h2 {
  margin-top: 20px;
  letter-spacing: 2px;
  margin: 0;
}
.wrapper p {
  margin-top: 10px;
}
.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}
.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:disabled {
  cursor: not-allowed;
  background: #746027;
}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
.Natija {
  height: 40%;
}
</style>
