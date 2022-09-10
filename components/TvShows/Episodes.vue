<template>
  <div>
    <div
      v-if="episodes.length > 0"
      class="accordion accordion-flush"
      id="accordionFlushExample"
    >
      <h1 class="container pb-4 mt-3" style="font-size: 50px">The Episodes</h1>
      <div v-for="episode in episodes" class="accordion-item" :key="episode.id">
        <h2 class="accordion-header" :id="`flush-heading${episode.id}`">
          <button
            style="font-weight: bold"
            class="accordion-button collapsed bg-light text-dark"
            type="button"
            data-bs-toggle="collapse"
            :data-bs-target="`#flush-collapse${episode.id}`"
            aria-expanded="false"
            :aria-controls="`flush-collapse${episode.id}`"
          >
            Season {{ episode.season }} Episode {{ episode.number }}
          </button>
        </h2>
        <div
          :id="`flush-collapse${episode.id}`"
          class="accordion-collapse collapse"
          :aria-labelledby="`flush-heading${episode.id}`"
          data-bs-parent="#accordionFlushExample"
        >
          <!-- Accordion Body -->
          <!-- Image -->
          <TvShowImage :episode="episode" />

          <!-- Summary -->
          <EpisodeSummary :episode="episode" />

          <!-- Details  -->
          <EpisodeDetails :episode="episode" />
        </div>
      </div>
    </div>
    <div v-else>
      <h1 style="font-size: 50px">No Episodes To Display</h1>
    </div>
  </div>
</template>

<script>
import TvShowImage from "./Episodes/Image.vue";
import EpisodeSummary from "./Episodes/Summary.vue";
import EpisodeDetails from "./Episodes/Details.vue";
export default {
  props: {
    episodes: Array,
  },
  components: {
    TvShowImage,
    EpisodeSummary,
    EpisodeDetails
  },
};
</script>
