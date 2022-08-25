
<template>
<div class="grid-container">
  <div class="route-container">
    <div class="input-group mb-3">
      <span class="input-group-text" id="inputGroup-sizing-default">From</span>
      <input v-model="cityChosen" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
    </div>
    <div class="input-group mb-3">
      <span class="input-group-text" id="inputGroup-sizing-default">To</span>
      <input type="text" v-model="desChosen" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
    </div>
    <label>Cargo dimension(in cm)</label>
    <div class="input-row mb-3">
      <label for="width" class="icon-width " > </label>
      <input type="text" id="width" class="dimension-size form-control" ><br><br>
      <label for="height" class="icon-height "> </label>
      <input type="text" id="height" class="dimension-size form-control"><br><br>
      <label for="depth" class="icon-depth"> </label>
      <input type="text" id="depth" class="dimension-size form-control"><br><br>
    </div>
    <div class="input-row mb-3">
      <label for="weight"  class="icon-weight "> </label>
      <input type="text" id="weight" class="dimension-size form-control"><br><br>
      <label for="category" class="icon-category dimension-size" ></label>
      <select name="category" id="category" class="form-control">
        <option value=""></option>
        <option value="clothes">Clothes</option>
        <option value="food">Food</option>
        <option value="animal">Animal</option>
        <option value="weapon">Weapon</option>
      </select>
    </div>
    <div class="input-row mb-3">
      <label for="date" class="icon-date" > </label>
      <input type="date" id="date"  class="form-control dimension-size"  style="width:80%" v-model="startDate"><br><br>
    </div>
    <div class="input-row input-group mb-3">
      <button id="search-button" class="form-control" @click="handleBooking">
        <div class="icon-search" style="margin-left:25%">
        </div>
      </button>
    </div>
    </div>
    <div id="map" style="width: 600px; height: 500px;"></div>
</div>
</template>
<script>
import L from 'leaflet';
import data from '../../data/dList.json'
import EventBus from '../event-bus.js';
import { required } from 'vuelidate/lib/validators'


export default {
  name:"MapComponent",
  data() {
    return {
      map: null,
      cityChosen: null,
      desChosen: null,
      width:null,
      height:null,
      depth:null,
      weight:null,
      category:null,
      startDate:null,
    };
  },
  validations: {
    cityChosen: {
      required,
    },
  },
  mounted () {
  this.map = L.map('map').setView([2.846482054534499, 18.56250107288361], 3),
  data.forEach((record) => {
		L.marker(record.longlat).addTo(this.map).on('click', () => {
      if (this.cityChosen) {
        this.desChosen = record.name
      } else {
        this.cityChosen = record.name
      }
    })
  }) 
	// this.map.on('click', function(e) {
  //   console.log(e.latlng)
	// });
	L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
		maxZoom: 19,
		attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
	}).addTo(this.map);
  },
  methods: {
    handleBooking() {
      console.log(this.$v)
      EventBus.$emit("handleModal");
    },
  },
};
</script>
