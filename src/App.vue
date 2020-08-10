<template>
  <div>
    <films-list
      :data="info"
    />

    <pagination-info
      :value="info"
      :count="countInfo"
    />
  </div>
</template>

<script>
  import FilmsList from "./components/FilmsList";
  import PaginationInfo from "./components/PaginationInfo";

  export default {
    name: 'App',
    components: {
      PaginationInfo,
      FilmsList,
    },
    data() {
      return {
        info: null,
        countInfo: 0,
        status: 0,
      };
    },
    props: {

    },
    mounted() {
      const axios = require('axios').default;

      axios
        .get('https://swapi.dev/api/films/')
        .then(response => {
          this.info = response.data.results;
          this.countInfo = response.data.count;
          this.status = response.status;
        });
    },
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
