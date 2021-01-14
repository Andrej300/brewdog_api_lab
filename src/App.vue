<template>
  <div id="app">
    
    <h1>Brewdog Beers!</h1>
    <!-- <ul>
    <li v-for="beer in allBrewDogBeers">{{ beer.name}}</li>
    </ul> -->
    <div class="main-container">
      <beer-list v-bind:allBrewDogBeers="allBrewDogBeers"></beer-list>
      <beer-detail v-bind:beer="selectedBeer"></beer-detail>
    
    </div>

  </div>
</template>

<script>
import { eventBus }  from './main.js'

import BeerList from './components/BeerList.vue'
import BeerDetail from './components/BeerDetail.vue'

export default {
  name: "App",
  data() {
    return {
      allBrewDogBeers: [],
      selectedBeer: null,
      favouriteBeers: []
    };
  },
  mounted(){ 
      fetch("https://api.punkapi.com/v2/beers")
      .then(response => this.allBrewDogBeers = response.json())
      .then(data => this.allBrewDogBeers = data);

      eventBus.$on('beer-selected', (beer) => {this.selectedBeer = beer});
      eventBus.$on('beer-favourite', (favBeer) => {this.favouriteBeers.push(favBeer)});
    },
  components: {
    'beer-list': BeerList,
    'beer-detail': BeerDetail
  },
  methods: {
    
  }
};
</script>

<style scoped>
.main-container{
  display:flex;
}
</style>
