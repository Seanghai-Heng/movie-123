<template>
  <div class="bg-black">
    <Loading v-if="loading" />

    <SearchResult v-else :searchResults="results" :searchText="tvShow" />

    <div class="pb-4"></div>

    <!-- Horizontal Line -->
    <Horizontal_Line />
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../components/Loading.vue";
import Horizontal_Line from "../components/Horizontal_Line.vue";
import SearchResult from "../components/Search/SearchResult.vue";
export default {
  name: "Search",
  created() {
    this.$nuxt.$on("search", ($event) => this.searchMovies($event));
  },
  data() {
    return {
      tvShow: this.$route.query.tvShow,
      results: [],
      loading: true,
    };
  },
  methods: {
    async moviesList() {
      const response = await axios.get(
        `https://api.tvmaze.com/search/shows?q=${this.tvShow}`
      );
      // console.log(response.data)
      this.results = response.data;
      this.loading = false;
    },
    searchMovies(val) {
      this.loading = true;
      this.tvShow = val;
      this.moviesList();
    },
  },
  mounted() {
    this.moviesList();
  },
  components: {
    Loading,
    SearchResult,
    Horizontal_Line,
  },
};
</script>

<style scoped>
.container {
  width: 80%;
}
.movie-poster {
  height: 300px;
}
.movie-list span {
  width: 100%;
}
.grid > .column1 > img {
  width: 350px;
  height: 250px;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
