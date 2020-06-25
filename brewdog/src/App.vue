<template>
  <div id="app">
    <div id="drop-list">
      <h1>Beers</h1>
      <label for="beer_select"></label>
      <select id="beer_select" v-model="selectedBeer">
        <option v-for="beer in beers" :value="beer">{{beer.name}}</option>
      </select>
    </div>
      <beer-detail :beer="selectedBeer"></beer-detail>
      <favourit-list></favourit-list>
  </div>
</template>

<script>
import BeerDetail from "./components/BeerDetail.vue";
import FavouriteList from "./components/FavouriteList.vue";

export default {
  name: "App",
  data() {
    return {
      beers: [],
      selectedBeer: null
    };
  },

  mounted() {
    for (let i = 1; i < 5; i++) {
      fetch(`https://api.punkapi.com/v2/beers?page=${i}&per_page=80`)
        .then(res => res.json())
        .then(jsonResponse => (this.beers = this.beers.concat(jsonResponse)));
    }
  },

  components: {
    "beer-detail": BeerDetail,
    "favourit-list": FavouriteList
  }
};
</script>

<style>
body {
  background-color: black;
  font-family: cursive;
}

h1 {
  color: rgb(251, 255, 0);
}

#app {
  text-align: center;
}

#drop-list {
  text-align: center;
  display: inline;
}

#beer_select {
  width: 420px;
  padding: 0.5rem 0;
  border: 1px solid #fff;
  border-radius: 18px;
  margin-bottom: 1rem;
  text-align: center;
  font-size: 1rem;
}
</style>