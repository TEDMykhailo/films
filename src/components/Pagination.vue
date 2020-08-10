<template>
  <div>
    <p>{{count}}</p>
  </div>
</template>

<script>
  export default {
    name: "Pagination",
    props: {
      count: Number,
    },
    data() {
      return {
        dataArray: null
      }
    },
    methods: {}
  }
</script>

<style scoped>

</style>
