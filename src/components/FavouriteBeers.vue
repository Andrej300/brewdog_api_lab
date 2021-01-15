<template lang="html">
    <div>
        <ul>
            <li v-for="(beer, index) in favouriteBeers" :key="index">
                Name: {{ beer.name }} - ABV: {{ beer.abv }} 
                <button @click="removeFromFavourites(beer)">x</button>  <!-- how do you pass to method?-->
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
            return this.allBeers.filter((beer) => beer.isFavourite);  //<-- this doesn't work?!
        },
    },
    props: ["allBeers"],
    methods: {
    removeFromFavourites: function(beer) {
        eventBus.$emit('beer-favourite-remove', beer)
    }
    }
};
</script>

<style scoped>
</style>