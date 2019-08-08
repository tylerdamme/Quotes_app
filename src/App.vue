<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <QuoteFilters/>
    <h1>Quotes</h1>
    <QuoteComponent v-for="quote in quotes" :quote="quote"/>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import axios from 'axios';
import QuoteComponent from './components/QuoteComponent.vue';
import QuoteFilters from './components/QuoteFilters.vue';

export default {
  name: 'app',
  components: {
    QuoteComponent,
    QuoteFilters,
    // HelloWorld
  },

  data() {
    return {
      quotes: [],
    }
  },

  mounted() {
    axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then (res => {
      let quoteResponse = res.data;
      for (let i = 0; i < quoteResponse.length; i++) {
        quoteResponse[i].id = i;
      }
      this.quotes = quoteResponse;
      console.log(this.quotes);
    });
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
