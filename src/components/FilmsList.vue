<template>
  <div>
    <div>
      <input
        type="text"
        v-model="search"
        placeholder="type here..."/>
      <input
        type="submit"
        @click="clearValue"
        value="Clear"/>
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
      :actorArray="film.customEl"
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
        perData: 4,
        pagination: {},
        name: null,
        newValue: '',
      }
    },
    methods: {
      clearValue(){
        this.search = ''
        console.log(this.search)
      },
      searchValue() {
        let this2 = this;
        return this.collection.filter(function (el) {
          if (el.title.includes(this2.search)) {
            return el.title.includes(this2.search)
          }
          let a = el.customEl.some(function (el2) {
            return el2.includes(this2.search)
          });
          if (a) {
            return el;
          }
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
      collection: function () {
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
