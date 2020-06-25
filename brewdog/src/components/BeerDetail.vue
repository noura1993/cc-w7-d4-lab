<template lang="html">
<div v-if="beer !== null" id="beer-detail">
    <h2>{{beer.name}}</h2>
    <img class="beer-img" :src="beer.image_url" alt="beer image">
    <h3>Ingredients:</h3>
    <div v-for="ingredient in getIngredients(beer)">
        {{ingredient}}
    </div>
    <button class="button" type="button" v-on:click="addToFavourite(beer.name)">Add To Fav</button>
</div>
</template>

<script>
import { eventBus } from "../main.js";

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
          if (seenIngredients.includes(ingredient) || ingredient == null) {
            return false;
          } else {
            seenIngredients.push(ingredient);
            return true;
          }
        });
    },

    addToFavourite: function(beer) {
      eventBus.$emit("add-beer", beer);
    }
  }
};
</script>

<style>
#beer-detail {
  font-size: 20px;
  background-color: rgb(255, 230, 0);
  width: 40%;
  margin: auto;
  margin-top: 5%;
  padding: 1%;
}

li {
  list-style: none;
}

.beer-img {
  width: 4%;
}

.button {
  cursor: pointer;
  width: 5.11rem;
  padding: .44rem 0;
  border-radius: 54px;
  background-color: black;
  text-align: center;
  font-size: .833rem;
  transition: background-color .25s;
  border: 0px;
  color: #fff;
  font-weight: 500;
  font-family: cursive;
  font-size: 15px;
}

.button:hover {
  background-color: rgb(212, 181, 5);
}
</style>
