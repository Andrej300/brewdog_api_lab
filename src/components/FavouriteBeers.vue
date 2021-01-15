<template>
  <div>
    <ul>
      <li v-for="(beer, index) in favouriteBeers" v-bind:key="index">
        Name: {{ beer.name }} - ABV: {{ beer.abv }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "favourite-beers",
  computed: {
    favouriteBeers: function () {
      return this.allBrewDogBeers.filter((beer) => beer.isFavourite);  //<-- this doesn't work?!
    },
  },
  props: ["allBrewDogBeers"],
};
</script>

<style scoped>
</style>