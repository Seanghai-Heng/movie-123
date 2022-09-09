<template>
  <div class="bg-black pt-4">
    <div v-if="loading" class="text-center">
      <div role="status">
        <svg
          class="inline mr-2 w-8 h-8 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
          viewBox="0 0 100 101"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
            fill="currentColor"
          />

          <path
            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
            fill="currentFill"
          />
        </svg>

        <span class="sr-only">Loading...</span>
      </div>
    </div>

    <div v-else class="text-white">
      <h2
        style="text-align: center; font-size: 40px; font-weight: bold"
        class="text-white"
      >
        {{ result.name }}
      </h2>
      <div class="card mb-4">
        <div class="overflow-hidden">
          <img
            v-if="result.image != null"
            class="w-full h-full transform hover:scale-125 duration-500"
            v-bind:src="result.image.medium"
          />
          <img v-else v-bind:alt="result.name" />
        </div>
        <h1 class="mt-2" v-if="result.country">
          Country : {{ result.country.name }}
        </h1>
        <p class="title" v-if="result.birthday">
          Birthday : {{ result.birthday }}
        </p>
        <p style="padding: 10px" v-if="result.gender">
          Gender : {{ result.gender }}
        </p>
      </div>

      <div
        v-if="castTvShows.length > 0 && castTvRefs.length > 0"
        class="container"
      >
        <!-- related tv show -->
        <h1 class="pb-4" style="font-size: 50px">Also Known For</h1>
        <div class="grid gap-4 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
          <div v-for="(castTvShow, index) in castTvShows" >
            <router-link :to="`/tvShows/${castTvShow.id}`">
              <div v-if="castTvRefs[index]" class="pb-3">
                <div
                  v-if="castTvRefs[index].image"
                  class="overflow-hidden d-flex justify-evenly items-center mb-3"
                  style="height: 300px"
                >
                  <img
                    width="300px"
                    class="w-full h-full transform hover:scale-125 duration-500"
                    :src="castTvRefs[index].image.medium"
                  />
                </div>
                    <div
                  v-else
                  class="overflow-hidden d-flex justify-evenly items-center mb-3"
                  style="height: 300px"
                >
                  <img v-bind:alt="castTvShow.name" />
                </div>
                
              </div>
            </router-link>

            <h1 class="text-lg text-center">
              <span class="fw-bold" v-if="castTvRefs[index]">
                {{ castTvRefs[index].name }}
              </span>
              in {{ castTvShow.name }}
            </h1>
          </div>
        </div>
      </div>
      <div v-else>
        <h1
          class="container pb-4"
          style="font-size: 50px"
          v-if="loading == false"
        >
          Doesn't Known For Any Movie
        </h1>
      </div>
    </div>
    <div
      class="flex pb-5 mx-auto px-3pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href:
            "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
        }
      ]
    };
  },
  name: "TV-Show-Casts",
  data() {
    return {
      id: this.$route.params.id,
      result: [],
      loading: true,
      castCredits: [],
      castTvShows: [],
      castTvRefs: []
    };
  },
  methods: {
    async showCastInfo() {
      const response = await axios.get(
        `https://api.tvmaze.com/people/${this.id}?embed=castcredits`
      );
      // console.log(response.data._embedded.castcredits);
      this.result = response.data;
      this.castCredits = response.data._embedded.castcredits;
    },
    async showCastCreditsInfo() {
      for (var i = 0; i < this.castCredits.length; i++) {
        await this.showCastMovieInfo(this.castCredits[i]._links.show.href);
        await this.showCastCharacterRef(this.castCredits[i]._links.character.href);
      }
      this.loading = false;
    },
    async showCastMovieInfo(url) {
      const response = await axios.get(url);
      this.castTvShows.push(response.data);
    },
    async showCastCharacterRef(url) {
      const response = await axios.get(url);
      this.castTvRefs.push(response.data);
    }
  },
  async mounted() {
    await this.showCastInfo();
    await this.showCastCreditsInfo();
  }
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 300px;
  margin: auto;
  text-align: center;
  font-family: arial;
}

.title {
  color: grey;
  font-size: 18px;
}
</style>
