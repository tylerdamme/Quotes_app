<template>
  <div>
    <button
      v-for="(category, index) in filterList"
      :item="category"
      :key="index"
      @click="filter = category;"
      :class="{ active: category == filter}"
      >
      {{ category }}
    </button>
  </div>
  
</template>

<script>
export default {
  name: 'QuoteFilters',
  data() {
    return {
      filterList: ["All", "Movies", "Games",],
      filter: "All",
    }
  }
}
</script>

