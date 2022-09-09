<template>
  <div class="text-white">
    <!-- Cast Info -->
    <CastInfo v-if="Object.keys(result).length > 0" :result="result" />

    <div v-else class="text-white text-center" style="font-size: 50px">
      No Result
    </div>

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
  </div>
</template>

<script>
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
    CastInfo,
    RelatedShows,
    CastResult,
  },
};
</script>
