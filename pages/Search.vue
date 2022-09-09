<template>
  <div class="bg-black">
    <!-- loading component -->
    <Loading v-if="loading" />
    <div v-else class="container pb-4 text-white">
      <div v-if="results.length == 0">
        <h1 class="text-lg">No Result</h1>
      </div>
      <h1 v-else style="font-size: 50px" class="text-center mb-2">
        Result Search For "{{ tvShow }}"
      </h1>
      <SearchResult :searchResults="results" />
    </div>
    <div class="pb-4"></div>
    <div
      class="flex pb-5 mx-auto px-3pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../components/Loading.vue";
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
