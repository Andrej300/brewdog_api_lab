<template>
  <div>
    <p v-on:click='clickBeer'>{{beer.name}}</p>

  </div>
</template>

<script>
import { eventBus }  from '../main.js'

export default {
    name: "beer",
    props: ['beer'],
    methods: {
        clickBeer: function() {
            // console.log(this.beer)
            eventBus.$emit('beer-selected', this.beer)
        }
    }

}
</script>

<style scoped> 

</style>