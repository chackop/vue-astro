<template>
  <div id="app">
    <AsteroidGrid
      @remove="remove"
      :asteroids="asteroids"
      header="Near-Earth Objects"
    />
  </div>
</template>

<script>
import AsteroidGrid from './components/AsteroidGrid.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    AsteroidGrid,
  },
  data() {
    return {
      asteroids: [],
    };
  },
  created: function() {
    this.fetchAsteroids();
  },
  methods: {
    fetchAsteroids: function() {
      var apiKey = '3326l6qhn8EcGO9h0LnUL6f5t7aitX53kNay73Hk';
      var url = 'https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=' + apiKey;
      axios.get(url).then((res) => {
        this.asteroids = res.data.near_earth_objects.slice(0, 10);
      });
    },
    remove: function(index) {
      this.asteroids.splice(index, 1);
    },
  },
};
</script>

<style>
[v-cloak] {
  display: none;
}
</style>
