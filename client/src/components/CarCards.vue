<template>
    <v-app>
        <v-row class="d-flex flex-wrap justify-center">
            <v-card v-for="(car, id) in this.cars" :key="id" style="width: 300px" class="ma-3 d-flex flex-column padding: 10px">
                <v-img :src="car.image"></v-img>
                <h1>
                    {{car.title}}
                </h1>
                <br>
                <span>
                    Owner: {{car.owner.firstName}} {{car.owner.lastName}}
                </span>
                <br>
                <span>
                    Year: {{car.yearOfMake}}
                </span>
                <span>
                    Miles: {{car.miles}}
                </span>
                <span>
                    Price: {{car.price}}
                </span>
                <br>
                <span>
                    {{car.description}}
                </span>
                <br>
                <v-btn :to="'/details/' + car.id" v-if="car.status != 'sold'" class="red" style="width: 100px">
                    Details
                </v-btn>
            </v-card>
        </v-row>
    </v-app>
</template>

<script>
import axios from "axios";
export default {
    data: () => ({
        cars: [],
        
    }),
    async created() {
        let response = await axios.get('http://localhost:3000/cars');
        this.cars = response.data;
        console.log(this.cars);
        console.log(this.response);
    }
}    
</script>