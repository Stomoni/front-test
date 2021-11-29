<template>
  <div class="home">
    <People v-bind:characters="this.characters" @characterDetail="characterDetail" @searchCharacter="searchCharacter"/>
  </div>
</template>

<script>
import axios from 'axios'
import People from '@/components/People.vue'

export default {
  name: 'Home',

  components: {
    People,
  },
  
  data() {
    return {
      characters: [],
    }
  },

  methods: {
    characterExist(name) {
      var selected = null;

      this.characters.forEach(c => {
        if (c.name == name) {selected = c}
      });
      return selected;
    },

    characterDetail(url) {
      var id = url.slice(29, url.length - 1);
      window.location.href = 'http://localhost:8080/character/' + id;
    },

    searchCharacter(input) {
      var url = "https://swapi.dev/api/people/?search=" + input
      axios.get(url)
      .then(res => {this.characters = res.data.results})
      .catch(e => console.log(e))
    }
  },

  created() {
    axios.get("https://swapi.dev/api/people/")
    .then(res => {this.characters = res.data.results;})
    .catch(e => {console.log(e)})
  }
}
</script>
