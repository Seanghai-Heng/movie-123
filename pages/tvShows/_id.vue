<template>
  <div class="bg-black pt-3">
    <!-- loading component -->
    <Loading v-if="loading" />

    <TvShowResult v-else :result="result" :casts="casts" :episodes="episodes" />
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../../components/Loading.vue";
import TvShowResult from "../../components/TvShows/Result.vue";

export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href: "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css",
          integrity:
            "sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC",
          crossorigin: "anonymous",
        },
      ],
      script: [
        {
          src: "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js",
          integrity:
            "sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM",
          crossorigin: "anonymous",
        },
        {
          src: "https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js",
        },
        {
          src: "http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js",
        },
      ],
    };
  },
  name: "movie",
  data() {
    return {
      id: this.$route.params.id,
      result: [],
      loading: true,
      casts: [],
      episodes: [],
    };
  },
  methods: {
    async showMovieInfo() {
      await axios
        .get(
          `https://api.tvmaze.com/shows/${this.id}?embed[]=episodes&&embed[]=cast`
        )
        .then(
          (response) => {
            this.result = response.data;
            this.casts = response.data._embedded.cast;
            this.episodes = response.data._embedded.episodes;
            this.loading = false;
          },
          (error) => {
            this.loading = false;
          }
        );
    },
  },
  mounted() {
    this.showMovieInfo();
  },
  components: {
    Loading,
    TvShowResult,
  },
};
</script>

<style scoped>
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
