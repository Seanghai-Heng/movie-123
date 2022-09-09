<template>
  <div>
    <div class="bg-black">
      <div class="container pb-4 text-white">
        <div class="p-5" v-if="result.length == 0">
          <h1 class="text-white text-center">No Result</h1>
          <Horizontal_Line />
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
  </div>
</template>

<script>
import Horizontal_Line from "../../components/Horizontal_Line.vue";
import Summary from "../../components/TvShows/Summary.vue";
import TvShowImage from "../../components/TvShows/Image.vue";
import TvShowDetails from "../../components/TvShows/Details.vue";
import Casts from "../../components/TvShows/Casts.vue";
import Episodes from "../../components/TvShows/Episodes.vue";
export default {
  props: {
    result: Object,
    episodes: Array,
    casts: Array,
  },
  components: {
    Summary,
    TvShowImage,
    TvShowDetails,
    Casts,
    Episodes,
    Horizontal_Line,
  },
  created() {
    console.log(this.result.length);
  },
};
</script>
