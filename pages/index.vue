<template>
  <div class="bg-black font-mono">
    <div class="container text-white">
      <div class="grid lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
        <!-- Tv show lists -->
        <div v-for="result in results" :key="result.id" class="movie-list p-4">
          <router-link :to="`/tvShows/${result.id}`">
            <div class="test relative">
              <div class="movie-poster overflow-hidden d-flex justify-evenly items-center" v-if="result.image">
                <img
                  v-if="result.image.medium"
                  class="w-full h-full  transform hover:scale-125 duration-500"
                  v-bind:src="result.image.medium"
                  v-bind:alt="result.name"
                />
              </div>
              <div v-else class="movie-poster overflow-hidden d-flex justify-evenly items-center">
                <img
                  v-bind:alt="result.name"
                />
              </div>
               <span class="absolute text-center">{{ result.name }}</span>
            </div>
          </router-link>
        </div>
        <!-- End tv show lists -->
      </div>
    </div>
    <div class="pb-4"></div>
    <div
      class="flex pb-5 mx-auto px-3pt-5 
            border-t border-gray-500 text-gray-400 text-sm 
            flex-col md:flex-row max-w-6xl"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      page: this.$route.query.page??0,
      results: [],
      loading: true
    };
  },
  methods: {
    async tvShowInfo() {
      await axios.get(`https://api.tvmaze.com/shows?page=${this.page}`).then(
        response => {
          this.results = response.data;
          this.loading = false;
          console.log(this.results);
        },
        error => {
          this.loading = false;
        }
      );
    }
  },
  mounted() {
    this.tvShowInfo();
    console.log(this.page)
  }
};
</script>

<style scoped>
a:hover{
  color: white;
}
.test {
  height: 300px;
}
.container {
  width: 80%;
}
.movie-poster {
  height: 300px;
}
.movie-list span {
  width: 100%;
}
</style>
