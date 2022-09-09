<template>
  <div class="bg-black">
    <!-- loading component -->
    <Loading v-if="loading" />

    <div v-else class="container pb-4 text-white">
      <div class="bg-white p-5" v-if="result.length == 0">
        <h1 class="text-black text-center">No Result</h1>
      </div>
      <div v-else>
        <!-- Summary Section -->
        <Summary :result="result" />

        <!-- Image Section -->
        <TvShowImage :result="result" />

        <!-- Movie Details Section -->
        <TvShowDetails :result="result" />

        <!-- Casts Section-->
        <Casts :casts="casts" />

        <!-- Horizontal Line -->
        <Horizontal_Line />

        <!-- Episodes Section -->
        <Episodes :episodes="episodes" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Loading from "../../components/Loading.vue";
import Horizontal_Line from "../../components/Horizontal_Line.vue";
import Summary from "../../components/TvShows/Summary.vue";
import TvShowImage from "../../components/TvShows/Image.vue";
import TvShowDetails from "../../components/TvShows/Details.vue";
import Casts from "../../components/TvShows/Casts.vue";
import Episodes from "../../components/TvShows/Episodes.vue";

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
      const response = await axios.get(
        `https://api.tvmaze.com/shows/${this.id}?embed[]=episodes&&embed[]=cast`
      );

      console.log(response.data._embedded.episodes);
      this.result = response.data;
      this.casts = response.data._embedded.cast;
      this.episodes = response.data._embedded.episodes;
      this.loading = false;
    },
  },
  mounted() {
    this.showMovieInfo();
  },
  components: {
    Loading,
    Summary,
    TvShowImage,
    TvShowDetails,
    Casts,
    Episodes,
    Horizontal_Line,
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
