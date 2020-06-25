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
  </div>
</template>

<script>
import BeerDetail from './components/BeerDetail.vue';

export default {
    name: "App",
    data(){
        return {
            beers: [],
            selectedBeer: null
        }
    },

  mounted() {
    for(let i=1; i<5; i++) {
      fetch(`https://api.punkapi.com/v2/beers?page=${i}&per_page=80`)
      .then(res => res.json())
      .then(jsonResponse => (this.beers = this.beers.concat(jsonResponse)));
    }

  },

  components: {
      "beer-detail": BeerDetail,
    }
}

</script>

<style>
body::after {
  background-size: cover;
  background-attachment: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  opacity: 0.5;
  z-index: -1;
  position: absolute;
  content: "";
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
  background-color: rgb(24, 150, 172);
  color: #fff;
}

</style>