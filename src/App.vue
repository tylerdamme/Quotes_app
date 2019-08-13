<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <QuoteFilters @buttonSelect="buttonSelect" :quotes="quotes"/>
    <SearchFilter @searchQuery="searchQuery"/>
    <h1>Quotes</h1>
    <div v-if="buttonQuotes.length === 0">
      <QuoteComponent v-for="quote in this.quotes" :quote="quote" :key="quote.id"/>
    </div>
    <div v-else>
      <QuoteComponent v-for="quote in this.buttonQuotes" :quote="quote" :key="quote.id"/>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import axios from 'axios';
import QuoteComponent from './components/QuoteComponent.vue';
import QuoteFilters from './components/QuoteFilters.vue';
import SearchFilter from './components/SearchFilter.vue';

export default {
  name: 'app',
  components: {
    QuoteComponent,
    QuoteFilters,
    SearchFilter,
    // HelloWorld
  },

  data() {
    return {
      quotes: [],
      buttonQuotes: [],
      // searchQuotes: [],
    }
  },

  mounted() {
    axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then (res => {
      let quoteResponse = res.data;
      for (let i = 0; i < quoteResponse.length; i++) {
        quoteResponse[i].id = i;
      }
      this.quotes = quoteResponse;
    });
  },

  methods: {
    buttonSelect(buttonQuotes) {
      this.buttonQuotes = buttonQuotes;
    },

    searchQuery(searchText) {
      if (searchText !== "") {
        this.buttonQuotes = ""
      };

      let results = this.quotes.filter(quote => {
        return quote.quote.toString().toLowerCase().includes(searchText.toLowerCase());
      });
      console.log(results);

    }
  }

}


</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
