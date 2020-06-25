<template>
  <div class="fav" v-if="favouriteList.length > 0">
    <h3>My Fav List</h3>
  <div v-for="beer in favouriteList">
    {{beer}}
    <button class="button" type="button" v-on:click="removeFromFav(beer)">Remove</button>
  </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "favourite-list",
  data() {
    return {
      favouriteList: []
    };
  },

  methods: {
    removeFromFav: function(beer) {
      let index = this.favouriteList.indexOf(beer);
      this.favouriteList.splice(index, 1);
    }
  },

  mounted() {
    eventBus.$on("add-beer", beer => {
      if (!this.favouriteList.includes(beer)) {
        this.favouriteList.push(beer);
      }
    });
  }
};
</script>

<style>

.fav {
  font-size: 25px;
  background-color: rgb(255, 230, 0);
  /* opacity: 0.8; */
  width: 40%;
  margin: auto;
  margin-top: 5%;
  padding: 1%;
}
</style>