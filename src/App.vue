<template>
  <div id="app">
    
    <h1>Brewdog Beers!</h1>
    <!-- <ul>
    <li v-for="beer in allBrewDogBeers">{{ beer.name}}</li>
    </ul> -->
    <div class="main-container">
      <beer-list v-bind:allBrewDogBeers="allBrewDogBeers"></beer-list>
      <div>
        <beer-detail v-bind:beer="selectedBeer" v-if="selectedBeer"></beer-detail>
        <!-- <favourite-beers v-bind:allBrewDogBeers="allBrewDogBeers"></favourite-beers> -->
      </div>
    
    </div>

  </div>
</template>

<script>
import { eventBus }  from './main.js'

import BeerList from './components/BeerList.vue'
import BeerDetail from './components/BeerDetail.vue'
import FavouriteBeers from './components/FavouriteBeers.vue'

export default {
  name: "App",
  components: {
    'beer-list': BeerList,
    'beer-detail': BeerDetail,
    'favourite-beers': FavouriteBeers
  },
  data() {
    return {
      allBrewDogBeers: [],
      // testGetAllBeers: [],
      selectedBeer: null
    };
  },
  methods:{
    // getAllBeers: async function() {
    //   let allData = [];
    //   let morePagesAvailable = true;
    //   let currentPage = 0;

    //   while(morePagesAvailable) {
    //     currentPage++;
    //     const response = await fetch(`https://api.punkapi.com/v2/beers?page=${currentPage}`)
    //     let { data, total_pages } = await response.json();
    //     data.forEach(e => allData.unshift(e));
    //     morePagesAvailable = currentPage < total_pages;
    //   }

    //   this.testGetAllBeers = allData;},

    addFavourBeer: function(beer) {
      const index = this.allBrewDogBeers.indexOf(beer);
      this.allBrewDogBeers[index].isFavourite = true; 
    },
    removeFavourBeer: function(beer) {
      const index = this.allBrewDogBeers.indexOf(beer);
      this.allBrewDogBeers[index].isFavourite = false;
    }
    },
  mounted(){ 
    // this.getAllBeers();
    
    fetch("https://api.punkapi.com/v2/beers")
    .then(response => this.allBrewDogBeers = response.json())
    .then(data => this.allBrewDogBeers = data);

    eventBus.$on('beer-selected', (beer) => {this.selectedBeer = beer});
    eventBus.$on('beer-favourite-add', beer => this.addFavourBeer(beer));
    eventBus.$on('beer-favourite-remove', beer => this.removeFavourBeer(beer));
    }
};
</script>

<style scoped>
.main-container{
  display:flex;
}
</style>
