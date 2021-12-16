<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''" >
    <v-col cols="12" align="center">
      <v-img
        src="https://images.pexels.com/photos/209831/pexels-photo-209831.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
        height="100vh"
      >
        <v-toolbar class="new" dark>
          <v-text-field
            hide-details
            prepend-icon="mdi-magnify"
            placeholder="Enter country Name..."
            v-model="city"
          ></v-text-field> </v-toolbar
        ><br />
        <v-btn v-on:click="Submit" class="button"> submit </v-btn>
        <div class="country-name">
          <h1
            v-if="weather && weather.name && weather.sys && weather.sys.country"
          >
            <p>{{ weather.name }}, {{ weather.sys.country }}</p>
          </h1>
          <br />
          <div v-if="weather && weather.main && weather.main.temp">
           <h1 class="temp" style=font-size:10vw>{{(Math.round(weather.main.temp)-273)+"&deg;C"}}</h1></div>
          <div
            v-if="
              weather &&
              weather.weather &&
              weather.weather.length &&
              weather.weather[0] &&
              weather.weather[0].main
            "
          >
            <h4>{{ weather.weather[0].main }}</h4>
          </div>
          <br />
        </div>
      </v-img>
    </v-col>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Home',
  data() {
    return {
      city: ' ',

      weather: {
        name:'city',sys:{country: 'country'},weather:[{main:'weather'}],main:{temp:'Temp'}
      },
    }
  },
  methods: {
    async Submit() {
      let result = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=e6dbb018942b5cd4d196d42e1886c8fa`
      )
      console.log('result', result)
      this.weather = result.data
      console.log('weather', this.weather)
    },
  },

  // dateBuil() {
  //   let d = new Date()
  //   let months = [
  //     'January',
  //     'February',
  //     'March',
  //     'April',
  //     'May',
  //     'June',
  //     'July',
  //     'August',
  //     'September',
  //     'October',
  //     'November',
  //     'December',
  //   ]
  //   let days = [
  //     'Sunday',
  //     'Monday',
  //     'Tuesday',
  //     'Wednesday',
  //     'Thursday',
  //     'Friday',
  //     'Saturday',
  //   ]
  //   let day = days[d.getDay()]
  //   let date = d.getDate()
  //   let month = months[d.getMonth()]
  //   let year = d.getFullYear()
  //   return `${day} ${date} ${month} ${year}`
  // },
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
.new {
  width: 50%;
  margin-top: 5%;
  border-radius: 10px;
}
.country-name {
  margin-top: 5%;
  border-radius: 10px;
  color: white;
  background-color: rgb(0, 0, 0, 0.6);
  height: 50%;
  width: 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
/* .button {
  color: green;
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: center;
} */
/* .temp{
  font-size: 1vw;
} */
#app.warm{
  background-image: src='http://www.pcctel.net/wp-content/plugins/awesome-weather/img/awe-backgrounds/drizzle.jpg';
}
</style>
