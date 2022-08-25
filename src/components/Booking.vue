
<template>
<div class="container">
   <h2 class="m-3"> Booking Information</h2>
    <div class="booking-container">
        <div v-for="booking in bookingList" class="  booking-record secondary" :key="booking.id">
            <!-- <div class="row p-2 m-2">
                ID: {{booking.id}}
            </div>
            <div class="my-row">
              <div class="">
              </div>
            </div> -->
            <div class="row  p-2 m-2">
            <div class="col-sm">
              From {{booking.source}}
            </div>
            <div class="col-sm">
              One of three columns
            </div>
            <div class="col-sm">
              One of three columns
            </div>
          </div>
        </div>
    </div>

</div>
</template>
<style>
.booking-container {
  max-width: 100%
}
</style>

<script>
import axios from "axios";

export default {
  name:"BookingComponent",
  data() {
    return {
        bookingList: [{
        "id": 1,
        "startDate": "2022-08-25T13:15:30",
        "source": "Congo",
        "destination": "Cairo",
        "arrivalDate": "2022-08-28T13:15:30",
        "category": "weapons"
    },
    {
        "id": 2,
        "startDate": "2022-08-25T13:15:30",
        "source": "Congo",
        "destination": "Cairo",
        "arrivalDate": "2022-08-28T13:15:30",
        "category": "weapons"
    },]
    };
  },
  mounted () {
      axios
        .get("https://wa-eit-dk1.azurewebsites.net/api/BookingModels",{header : { "Access-Control-Allow-Origin": true, 'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8'}
        })
        .then((response) => {
          this.info = response.data.bpi;
        })
        .catch((error) => {
          console.log(error);
          this.errored = true;
        });
  },
  methods: {

  },
};
</script>
