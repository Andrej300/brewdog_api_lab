<template>
    <div>
<ul>
    <li v-for="beer in favBeers"> Name: {{beer.name}} - ABV: {{beer.abv}} </li>
</ul>



    </div>
</template>

<script>
    export default {
        name:"favourite-beers",
        props:['favBeers']
        
    }
</script>

<style scoped>

</style>