<template>
  <div class="container" style="margin-top: 15px">
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
  import { BootstrapVue, BootstrapVueIcons } from 'bootstrap-vue'

  import 'bootstrap/dist/css/bootstrap.css'
  import 'bootstrap-vue/dist/bootstrap-vue.css'

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
          })
        })
        return this.newData;
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
