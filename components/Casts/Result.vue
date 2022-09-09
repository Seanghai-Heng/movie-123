<template>
  <div class="text-white">
    <!-- Cast Info -->
    <CastInfo :result="result" />

    <div
      v-if="castTvShows.length > 0 && castTvRefs.length > 0"
      class="container pb-4"
    >
      <!-- related tv show -->
      <RelatedShows :castTvShows="castTvShows" :castTvRefs="castTvRefs" />
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
</template>

<script>
import Horizontal_Line from "../../components/Horizontal_Line.vue";
import CastResult from "../../components/Casts/Result.vue";
import CastInfo from "../../components/Casts/CastInfo.vue";
import RelatedShows from "../../components/Casts/RelatedShows.vue";
export default {
  props: {
    result: Object,
    castCredits: Array,
    castTvShows: Array,
    castTvRefs: Array,
  },
  components: {
    Horizontal_Line,
    CastInfo,
    RelatedShows,
    CastResult,
  },
};
</script>
