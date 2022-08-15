<template>
  <div>
    <SearchJokes v-on:search-text="searchText"></SearchJokes>
    <Joke v-for="joke in jokes"
          v-bind:key="joke.id"
          :key="joke.id"
          :joke="joke.joke"
          :id="joke.id"
    />
  </div>
</template>


<script>
import axios from "axios";
import Joke from "@/components/Joke";
import SearchJokes from "@/components/SearchJokes";

export default {
  components: {
    Joke
  },

  data() {
    return {
      jokes: []
    };
  },

  async created() {
    const config = {
      headers: {
        Accept: 'application/json'
      }
    };

    try {
      const response = await axios.get('https://icanhazdadjoke.com/search', config);

      this.jokes = response.data.results;

    } catch (error) {
      console.log(error);
    }

  },

  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: 'application/json'
        }
      };

      try {
        const response = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);

        this.jokes = response.data.results;
      } catch (error) {
        console.log(error);
      }
    },
  },

  head() {
    return {
      title: 'Dad Jokes',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: "Best place to find Dad Jokes"
        }
      ]
    };
  }
};
</script>

<style>

</style>
