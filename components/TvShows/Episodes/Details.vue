<template>
  <div class="accordion-body text-dark">
    <p>
      <span class="fw-bold">Episode's Name: </span>
      {{ episode.name }}
    </p>
    <p>
      <span class="fw-bold">Episode's Type: </span>
      {{ episode.type }}
    </p>
    <p><span class="fw-bold">Air Date: </span> {{ episode.airdate }}</p>
    <p>
      <span class="fw-bold">Run Time: </span>
      {{ episode.runtime }} minutes
    </p>
    <p>
      <span class="fw-bold" v-if="episode.rating.average"
        >Rating: {{ episode.rating.average }}</span
      >
      <span class="fw-bold" v-else>Rating: "No Rating"</span>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    episode: Object,
  },
};
</script>
