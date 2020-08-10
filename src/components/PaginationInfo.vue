<template>
  <div>
    <p>{{count}}</p>
    <hr/>
    <ul>
      <li v-for="item in collection">
        {{item}}
      </li>
    </ul>
    <hr/>
    <div>
      <div>
        <button v-for="p in pagination.pages" @click.prevent="setPage(p)">
          {{p}}
        </button>
      </div>
    </div>
    <div>
      <p>
        {{pagination.startIndex}} to {{pagination.endIndex}}
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    name: "PaginationInfo",
    props: {
      count: Number,
      value: Array,
    },
    data() {
      return {
        data: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11],
        dataArray: null,
        perData: 4,
        pagination: {},
      }
    },
    methods: {
      setPage(p) {
        this.pagination = this.paginator(this.data.length, p)
      },
      paginate(data) {
        return data.slice(this.pagination.startIndex, this.pagination.endIndex + 1)
      },
      paginator(totalItems, currentPage) {
        let startIndex = (currentPage - 1) * this.perData;
        let endIndex = Math.min(startIndex + this.perData - 1, totalItems - 1)
        console.log(startIndex, endIndex)

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
    created(){
      this.setPage(1);
    }
  }
</script>

<style scoped>

</style>
