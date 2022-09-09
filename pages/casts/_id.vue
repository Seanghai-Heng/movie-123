<template>
  <div class="bg-black pt-4">
    <Loading v-if="loading" />

    <CastResult
      v-else
      :result="result"
      :castTvShows="castTvShows"
      :castTvRefs="castTvRefs"
    />
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../../components/Loading.vue";
import CastResult from "../../components/Casts/Result.vue";
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
      await axios
        .get(`https://api.tvmaze.com/people/${this.id}?embed=castcredits`)
        .then(
          (response) => {
            this.result = response.data;
            this.castCredits = response.data._embedded.castcredits;
            this.loading = false;
          },
          (error) => {
            this.loading = false;
          }
        );
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
    CastResult,
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
</style>
