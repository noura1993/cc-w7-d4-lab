<template lang="html">
<div v-if="beer !== null" id="beer-detail">
    <h2>{{beer.name}}</h2>
    <p>Ingredients: {{getIngredients(beer)}}</p>
    <img class="beer-img" :src="beer.image_url" alt="beer image">
</div>
</template>

<script>
export default {
    name: "beer-detail",
    props: ["beer"],
    methods: {
        getIngredients: function(beer) {
            let seenIngredients = [];
            return Object.values(beer.ingredients)
            .flat()
            .map(ingredient => ingredient.name)
            .filter(ingredient => {
                if(seenIngredients.includes(ingredient) || ingredient == null) {
                    return false;
                } else {
                    seenIngredients.push(ingredient);
                    return true;
                }
            })
        }
    }
}

</script>

<style>
.beer-img {
    width: 4%;
}
</style>
