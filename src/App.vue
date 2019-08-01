<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Quotes</h1>
    <li v-for="quote in quotes">
      <h2>{{quote.id + 1}}</h2>
      <p>{{quote.context}}</p>
      <p>{{quote.quote}}</p>
      <p>{{quote.source}}</p> 
    </li>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  components: {
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
