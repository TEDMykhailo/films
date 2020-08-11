<template>
  <div>
    <films-list
      v-if="info"
      :data="info"
      :count="countInfo"
      :someData="getInfoValue(data)"
      :someInfo="integrationData(info, someData)"
    />
  </div>
</template>

<script>
  import FilmsList from "./components/FilmsList";

  export default {
    name: 'App',
    components: {
      FilmsList,
    },
    data() {
      return {
        info: null,
        countInfo: 0,
        status: 0,
        data: null,
        urlFilm: '',
        someData: [],
        newData: [],
      };
    },
    props: {},
    mounted() {
      const axios = require('axios').default;

      axios
        .get('https://swapi.dev/api/films/')
        .then(response => {
          this.info = response.data.results;
          this.countInfo = response.data.count;
          this.status = response.status;
        });

      axios
        .get('https://swapi.dev/api/people/')
        .then(response => this.data = response.data.results);

    },
    methods: {
      getInfoValue() {
        return this.someData = this.data.map(function (el) {
          let newArr = [
            el.name,
            el.films,
          ]
          return newArr;
        })
      },
      integrationData(valueInfo, valueData) {
        this.newData = valueInfo.map(function (el) {
          el.customEl = [];
          let a = valueData.map(function (el2) {
            if(el2[1].some(searchEl => searchEl === el.url)){
              el.customEl.push(el2[0])
            }
            // console.log(el.url)
            // console.log(el2)
          })
          console.log(el)
          // return el.url;
        })
        return this.newData;
      },
      // searchDataValue(valueData, value) {
      //   return valueData.filter(el => {
      //     return el.films.some(elFilms => elFilms === value)
      //   })
      // }
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
