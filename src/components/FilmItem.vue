<template>
  <div>
    <h3>Title: {{title}}</h3>
    <p>Director: {{director}}</p>
    <p>Producer: {{producer}}</p>
    <p>Release date: {{release_date}}</p>
    <p>Opening crawl: {{opening_crawl}}</p>
    <p><b>Actors: </b><span v-for="(item, index) in actorArray">{{actorArray.length -1 == index ? item: item + ', '}}</span>
    </p>
    <hr/>
  </div>
</template>

<script>
  export default {
    name: "FilmItem",
    props: {
      film: Object,
      director: String,
      title: String,
      release_date: String,
      producer: String,
      opening_crawl: String,
      actorArray: Array,
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
