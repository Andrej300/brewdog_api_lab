<template>
  <div id="app">
    
    <h1>Brewdog Beers!</h1>
    <!-- <ul>
    <li v-for="beer in allBrewDogBeers">{{ beer.name}}</li>
    </ul> -->
    <div class="main-container">
      <beer-list v-bind:allBeers="allBrewDogBeers"></beer-list>
      <div>
        <beer-detail :beer="selectedBeer" v-if="selectedBeer"></beer-detail>
        <favourite-beers v-if="Array.isArray(allBrewDogBeers)" :allBeers="allBrewDogBeers"></favourite-beers>
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

    // to test, look up the fetch reply natively.  This is what returns a promise, what does as promise of nothing look like?
    // loop through fetch commands while the promise doesnt look empty, when it does, do a promise.all etc...


    // getAllBeers:  function() {
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

    //   this.allBrewDogBeers = allData;
    // },

    addFavourBeer: function(beer) {
      const index = this.allBrewDogBeers.indexOf(beer);
      this.allBrewDogBeers[index].isFavourite = true;
      this.allBrewDogBeers = [...this.allBrewDogBeers];
    },
    removeFavourBeer: function(beer) {
      console.log(beer)
      const index = this.allBrewDogBeers.indexOf(beer);
      this.allBrewDogBeers[index].isFavourite = false;
      this.allBrewDogBeers = [...this.allBrewDogBeers];
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
