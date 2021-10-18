<template>
  <v-app>
    <LogoBar></LogoBar>
    <v-main>
      <v-container>
        <router-view :cars="cars"></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import LogoBar from './views/LogoBar';
import axios from "axios";
export default {
  name: 'App',
  data: () => ({
    cars: [],

  }),
   async created() {
        let response = await axios.get('http://localhost:3000/cars');
        this.cars = response.data;
        console.log(this.cars);
        console.log(this.response);
    },
  components: {
    LogoBar,
  }
};
</script>
