<template>
  <div class="bg-black pt-4">
    <Loading v-if="loading" />
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
        class="container pb-4"
      >
        <!-- related tv show -->
        <h1 class="pb-4" style="font-size: 50px">Also Known For</h1>
        <div class="grid gap-4 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
          <div v-for="(castTvShow, index) in castTvShows">
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
      <!-- Horizontal Line -->
      <Horizontal_Line />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../../components/Loading.vue";
import Horizontal_Line from "../../components/Horizontal_Line.vue";
export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href: "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css",
        },
      ],
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
      castTvRefs: [],
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
        await this.showCastCharacterRef(
          this.castCredits[i]._links.character.href
        );
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
    },
  },
  async mounted() {
    await this.showCastInfo();
    await this.showCastCreditsInfo();
  },
  components: {
    Loading,
    Horizontal_Line,
  },
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
