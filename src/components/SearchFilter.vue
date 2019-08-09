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
  }
}
</script>
