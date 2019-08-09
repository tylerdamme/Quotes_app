<template>
  <div>
    <button
      v-for="(category, index) in filterList"
      :item="category"
      :key="index"
      @click="selection(category);"
      >
      {{ category }}
    </button>
  </div>
  
</template>

<script>
export default {
  name: 'QuoteFilters',
  props: ['quotes'],
  data() {
    return {
      filterList: ["all", "movies", "games",],
      buttonQuotes: [],
      category: 'all',
    }
  },
  methods: {
    selection(category) {
      this.buttonQuotes = this.quotes
      if (category === "all") {
        this.buttonQuotes = this.quotes;
      } else { 
        this.buttonQuotes = this.quotes.filter(quote => quote.theme === category);
      }
      this.$emit('buttonSelect', this.buttonQuotes);
    }
  }
}
</script>

