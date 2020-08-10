<template>
  <div>
    <film-item
      v-for="film in data"
      :director="film.director"
      :title="film.title"
      :release_date="film.release_date"
      :producer="film.producer"
      :opening_crawl="film.opening_crawl"
    />
  </div>
</template>

<script>
  import FilmItem from "./FilmItem";

  export default {
    name: "FilmsList",
    data() {
      return {
        name: null,
      }
    },
    props: {
      data: Array,
    },
    components: {FilmItem},
    methods: {
      getData() {
        return this.data;
      }
    }
  }
</script>

<style scoped>

</style>
