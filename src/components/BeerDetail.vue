<template>
<div> 

<h1>Clicked beer name: {{ beer.name}}</h1>
<h2>Clicked beer percentage: {{ beer.abv }} </h2>
<img v-bind:src="beer.image_url" id="beer">

</div>
</template>

<script>
export default { 
    name: "beer-detail",
    props: ['beer']
    

}
</script>

<style scoped> 
#beer { 
    max-height: 150px;
}
   

</style> 