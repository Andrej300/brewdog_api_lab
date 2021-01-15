<template>
<div>
    <ul>
    <li v-for="(beer, index) in favouriteBeers" v-bind:value="beer" v-bind:key="index">
        Name: {{ beer.name }} - ABV: {{ beer.abv }} 
        <button v-on:click="removeFromFavourites(favouriteBeers[index] || beer)">x</button>  <!-- how do you pass to method?-->
    </li>
    </ul>
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
    removeFromFavourites: function(beer) {
        eventBus.$emit('beer-favourite-remove', beer)
    }
    }
};
</script>

<style scoped>
</style>