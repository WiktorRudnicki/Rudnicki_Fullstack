<template>
  <div class="d-flex justify-center">
    <v-card class="ma-5 d-flex flex-column justify-end" style="width:400px">
      <v-img :src="filtration.image"></v-img>
      <div class="text-h4 my-2 d-flex justify-center">
        {{ filtration.title }}
      </div>
      <v-simple-table>
        <thead>
          <tr>
            <th>Price</th>
            <th>Miles</th>
            <th>Year of Make</th>
            <th>Current Owner</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ filtration.price }}</td>
            <td>{{ filtration.miles }}</td>
            <td>{{ filtration.yearOfMake }}</td>
            <td>{{ filtration.owner.firstName }} {{ filtration.owner.lastName }}</td>
          </tr>
        </tbody>
      </v-simple-table>
      <p>{{ filtration.description }}</p>
      <div class="d-flex mb-3">
        <v-btn class=" purple 2 white--text" to="/">Go back</v-btn>
        <v-spacer></v-spacer>
        <v-btn class=" red darken 2 white--text" @click="buy" v-if="filtration.status != 'sold'">Order</v-btn>
      </div>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {};
  },
  props: {
    id: {
      type: String
    },
    cars: {
      type: Array
    }
  },
  computed: {
    filtration() {
      return this.cars.find(el => el.id == this.id);
    }
  },
  methods: {
    async buy(event) {
      event.title += " RESERVED!";
      await axios({
        method: "PATCH",
        url: `http://127.0.0.1:3000/cars/${this.id}`,
        "content-type": 
        "application/json",
        data: { status: "sold" }
      });
      this.$router.go();
    }
  }
};
</script>