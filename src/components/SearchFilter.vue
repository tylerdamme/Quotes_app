<template>
  <input type="text" v-model="search" placeholder="Search quotes">
</template>

<script>
export default {
  name: 'SearchFilter',
  data() {
    return {
      search: ''
    }
  },

  watch: {
    search(input) {
      this.$emit('searchQuery', input);
    }
  }
}
</script>
