<template>
  <div>
    <div>
      <input
        v-model="search"
        type="search"
        placeholder="type here...">
      <button @click="searchValue">Search</button>
      <p>{{search}}</p>
    </div>
    <film-item
      v-if="collection"
      v-for="film in searchValue()"
      :director="film.director"
      :title="film.title"
      :release_date="film.release_date"
      :producer="film.producer"
      :opening_crawl="film.opening_crawl"
    />
    <div>
      <button v-for="p in pagination.pages" @click.prevent="setPage(p)">
        {{p}}
      </button>
    </div>
    <div>
      <p>
        {{pagination.startIndex + 1}} to {{pagination.endIndex + 1}}
      </p>
    </div>
  </div>
</template>

<script>
  import FilmItem from "./FilmItem";

  export default {
    name: "FilmsList",
    props: {
      count: Number,
      data: Array,
    },
    components: {FilmItem},
    data() {
      return {
        search: '',
        dataArray: null,
        perData: 2,
        pagination: {},
        name: null,
      }
    },
    methods: {
      searchValue() {
        return this.collection.filter(el => {
          return el.title.includes(this.search)
        });
      },
      setPage(p) {
        this.pagination = this.paginator(this.data.length, p)
      },
      paginate(data) {
        return data.slice(this.pagination.startIndex, this.pagination.endIndex + 1)
      },
      paginator(totalItems, currentPage) {
        let startIndex = (currentPage - 1) * this.perData;
        let endIndex = Math.min(startIndex + this.perData - 1, totalItems - 1)

        return {
          currentPage: currentPage,
          startIndex: startIndex,
          endIndex: endIndex,
          pages: _.range(1, Math.ceil(totalItems / this.perData) + 1)
        }
      },
    },
    computed: {
      collection() {
        return this.paginate(this.data)
      }
    },
    created() {
      this.setPage(1);
    }
  }
</script>

<style scoped>

</style>
