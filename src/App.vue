<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <QuoteFilters @buttonSelect="buttonSelect" :quotes="quotes"/>
    <SearchFilter @searchQuery="searchQuery"/>
    <h1>Quotes</h1>
      <QuoteComponent v-for="quote in paginatedData" :quote="quote" :key="quote.id"/>
    <button @click="prevPage" :disabled="pageNumber == 0">
      Previous
    </button>
    <button @click="nextPage" :disabled="pageNumber >= pageCount -1">
      Next
    </button>
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
      quoteData: [],
      pageNumber: 0,
      size: 15,
    }
  },

  mounted() {
    axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then (res => {
      let quoteResponse = res.data;
      for (let i = 0; i < quoteResponse.length; i++) {
        quoteResponse[i].id = i;
      }
      this.quotes = quoteResponse;
      this.quoteData = this.quotes;
    });
  },

  methods: {
    buttonSelect(buttonQuotes) {
      this.pageNumber = 0;
      this.quoteData = this.quotes;
      this.quoteData = buttonQuotes;
    },

    searchQuery(searchText) {
      this.pageNumber = 0;
      if (searchText !== "") {
        this.buttonQuotes = ""
      };

      let results = this.quotes.filter(quote => {
        return quote.quote.toString().toLowerCase().includes(searchText.toLowerCase());
      });

      this.quoteData = results;

    },

    nextPage() {
      this.pageNumber++;
    },

    prevPage() {
      this.pageNumber--;
    },
  },

  computed: {
    pageCount() {
      let l = this.quoteData.length;
      let s = this.size;
      return Math.ceil(l / s);
    },

    paginatedData() {
      const start = this.pageNumber * this.size;
      const end = start + this.size;

      return this.quoteData.slice(start, end);
    },
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
