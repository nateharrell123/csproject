<template>
    <!-- <svg class="searchIcon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" 
    fill="none" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
    v-show="isRadiusSearch">
    <circle cx="11" cy="11" r="8"></circle>
    <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
    </svg> -->
  <div class="selectField">
    <select class="selectClass" v-model="searchType" @change="selectChanged($event)">
      <option value="" disabled selected>Choose a search method:</option>
      <option value="SearchNearby">Search nearby</option>
      <option value="SearchSpecific">Search specific</option>
    </select>
  </div>

  <div class="centeredRadiusSearch">
    <div class="radiusDiv">
      <input style="width: 407px;"
      v-show="isRadiusSearch"
      class="radiusSearch" 
      placeholder="Enter a radius (mi.):"
      v-model="radius"
      v-on:keyup.enter="findNearby"
      maxlength="2"
      >

    </div>
    <div class="nearbySelect">
      <select class="selectClass" 
      v-model="nearbyFilterType" @change="radiusFilterChanged($event)" style="width: 402px;"
      v-show="isRadiusSearch">
      <option value="" disabled selected>Establishment type:</option>
        <option value="restaurant">Restaurants</option>
        <option value="bar">Bars</option>
        <option value="department_store">Grocery/Shopping</option>
        <option value="movie_theater">Movie Theatres</option>
      </select>
    </div>
  </div>
  
    <!-- <div class="centeredRadiusSearch">     Old autocomplete
      <GMapAutocomplete
      style="width: 600px;"
      v-show="isSpecificSearch"
      class="specificSearch"
      id="specificSearch"
      @place_changed="setPlace"
      placeholder="Search for a place: "
      ></GMapAutocomplete>
    </div> -->

    <div class="centeredRadiusSearch">
      <SpecificSearch
      :SpecificData="specificData"
      v-if="specificIsLoaded"
      />
    </div>

    <div class="results">
      <ResultsTable
      :SearchResults="places"
      v-if="nearbyIsLoaded"
      />
    </div>

</template>

<script>
import SpecificSearch from "./SpecificSearch.vue";
import ResultsTable from "./ResultsTable.vue";
import VueGoogleMaps from '@fawmi/vue-google-maps'

export default {
  data() {
    return {
      name: "Search",
      coordinates: {
        lat: 0,
        lng: 0
      },
      nearbyFilterType: "",
      radius : null,
      nearbyIsLoaded : false,
      specificIsLoaded : false,
      places: [],
      isRadiusSearch : false,
      isSpecificSearch : false,
      searchType: "",
      specificData : {},
      gmap: {}
    }
  },

  components : {
    ResultsTable,
    SpecificSearch
  },

  mounted : function (){
    this.grabLocation()
    //this.map = new VueGoogleMaps.gmapApi.maps.LatLng(this.coordinates.lat, this.coordinates.lng);

    //var element = document.getElementById("specificSearch");
    //element.addEventListener("blur", function() { this.findNearby()});


  },

  /* Functions */
  methods: {
    grabLocation() {
      this.$getLocation()
        .then((coordinates) => {
          this.coordinates = {
            lat: coordinates.lat,
            lng: coordinates.lng,
          };
      //console.log(this.coordinates.lat);
        })
        .catch((error) => alert(error));
    },
    setPlace(placeResultData){ // gross
      this.specificData = placeResultData
      this.specificIsLoaded = !this.specificIsLoaded
      this.nearbyIsLoaded = false
    },
    findNearby() {

















      // this.specificIsLoaded = false;
      
      // var axios = require("axios");
      // var config = {
      //   method: "get",
      //   url: `https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=${this.coordinates.lat},${this.coordinates.lng}&radius=${this.radius * 1000}&type=${this.nearbyFilterType}&key=AIzaSyDASvg4ATeMQcAsocmem5kFdTMDw_NSJwo`,
      // };
      // let self = this; // strange :P
      // axios(config)
      //   .then(function (response) {
      //     console.log(JSON.stringify(response.data));
          
      //     self.places = response.data.results;
      //     if (self.isSpecificSearch)
      //     {
      //       self.specificIsLoaded = true;
      //     }
      //     else if (self.isRadiusSearch)
      //     {
      //       self.nearbyIsLoaded = true;
      //     }
      //   })
      //   .catch(function (error) {
      //     console.log(error);
      //   });
    },
    callback(results, status){
      if (status == VueGoogleMaps.gmapApi.maps.places.PlacesServiceStatus.OK) {
        this.places = results
      }
    },
    selectChanged(){
        if (event.target.value === "SearchSpecific")
        {
          this.isSpecificSearch = !this.isSpecificSearch;
          
          this.isRadiusSearch = false;
        }
        if (event.target.value === "SearchNearby")
        {
          this.isRadiusSearch = !this.isRadiusSearch;
          this.isSpecificSearch = false;
        }
    },

    radiusFilterChanged(){
      this.findNearby()
    }
  },
};
</script>

<style scoped>

.hide, map{
  display:none;
}
.radiusSearch{
  margin-top:10px;
  font-size: 1.5rem;
  padding: 15px 45px 15px 30px;
	font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
  font-weight: 300;
  box-sizing: border-box;
  letter-spacing: 2px;
  color: rgba(0, 0, 0, 0.5);
}
.searchIcon{
    cursor: pointer;
}
.specificSearch{
  margin-top:10px;
  font-size: 1.5rem;
  padding: 15px 45px 15px 30px;
	font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
  font-weight: 300;
  box-sizing: border-box;
  letter-spacing: 2px;
  color: rgba(0, 0, 0, 0.5);
}
.centeredRadiusSearch{
  text-align:center;
}
.radiusDiv{
  display:inline-block;
  padding-right:40px;
}
.selectClass{
  display:block;
  margin:auto;
  margin-top:20px;
  font-size: 1.5rem;
  padding: 15px 45px 15px 30px;
	font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
  font-weight: 300;
  box-sizing: border-box;
  letter-spacing: 2px;
  color: rgba(0, 0, 0, 0.5);
}
.nearbySelect{
  display:inline-block;
}
.selectField{
  padding-bottom:20px;
}
.results{
  text-align: -webkit-center;
}

.box {
  font-size: 20px;
}
</style>