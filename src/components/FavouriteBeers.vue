<template>
  <div>
    <ul>
      <li v-for="(beer, index) in favouriteBeers" v-bind:value="beer" v-bind:key="index">
        Name: {{ beer.name }} - ABV: {{ beer.abv }} 
        <button v-on:click="removeFromFavourites$beer[index]" v-bind:value="allBrewDogBeers[index]">x</button>  <!-- how do you pass to method?-->
    </ul>
       </li> 
  </div>
</template>

<script>
import { eventBus }  from '../main.js'
export default {
  name: "favourite-beers",
  computed: {
    favouriteBeers: function () { 
      return this.allBrewDogBeers.filter((beer) => beer.isFavourite);  //<-- this doesn't work?!
    },
  },
  props: ["allBrewDogBeers"],
  methods: {
    removeFromFavourites: function() {
        eventBus.$emit('beer-favourite-remove', this.beer)
    }
    }
};
</script>

<style scoped>
</style>