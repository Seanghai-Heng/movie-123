<template>
  <div class="bg-black">
    <!-- loading component -->
    <Loading  v-if="loading"/>
    <div v-else class="container pb-4 text-white">
      <div v-if="results.length == 0">
        <h1 class="text-lg">No Result</h1>
      </div>
      <h1 v-else style="font-size: 50px" class="text-center mb-2">
        Result Search For "{{ tvShow }}"
      </h1>
      <div
        v-for="result in results"
        :key="result.id"
        class="grid md:grid-cols-3 mb-4 items-center"
      >
        <div class="movie-list p-4">
          <router-link :to="`/tvShows/${result.show.id}`">
            <div
              class="movie-poster overflow-hidden d-flex justify-evenly items-center"
            >
              <img
                v-if="result.show.image != null"
                class="w-full h-full transform hover:scale-125 duration-500"
                v-bind:src="result.show.image.medium"
                v-bind:alt="result.show.name"
              />
              <img v-else v-bind:alt="result.show.name" />
            </div>
          </router-link>
        </div>
        <div class="column2 col-span-2 leading-10 ml-4 text-lg">
          <div class="details">
            <ul>
              <li>Movie Name : {{ result.show.name }}</li>
              <li v-if="result.show.rating.average">
                Rating : {{ result.show.rating.average }}
              </li>
              <li v-else>Rating : No Rating</li>
              <li
                v-if="result.show.schedule.days[0] && result.show.schedule.time"
              >
                Schedule : {{ result.show.schedule.days[0] }} at
                {{ result.show.schedule.time }}
              </li>
              <li v-else>Schdule : Not available</li>
              <li v-if="result.show.runtime">
                Runtime : {{ result.show.runtime }} mns
              </li>
              <li v-else>Runtime : Not available</li>
              <li>Status : {{ result.show.status }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="pb-4"></div>
    <div
      class="flex pb-5 mx-auto px-3pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../components/Loading.vue"
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
  components:{
    Loading
  }
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
