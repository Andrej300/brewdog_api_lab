<template>
<div> 

<h1>Clicked beer name: {{ beer.name}}</h1>
<h2>Clicked beer percentage: {{ beer.abv }} </h2>
<img v-bind:src="beer.image_url" id="beer">
<button v-on:click="addToFavourites">Add to favourites</button>
</div>
</template>

<script>
import { eventBus }  from '../main.js'

export default { 
    name: "beer-detail",
    props: ['beer'],
    methods: {
    addToFavourites: function() {
        eventBus.$emit('beer-favourite', this.beer)
    }
    }
    

}
</script>

<style scoped> 
#beer { 
    max-height: 150px;
}
   

</style> 