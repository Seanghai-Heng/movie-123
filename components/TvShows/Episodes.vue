<template>
  <div>
    <div
      v-if="episodes.length > 0"
      class="accordion accordion-flush"
      id="accordionFlushExample"
    >
      <h1 class="container pb-4 mt-3" style="font-size: 50px">The Episodes</h1>
      <div v-for="episode in episodes" class="accordion-item">
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
          <div class="accordion-body text-dark">
            <div class="overflow-hidden d-flex justify-evenly items-center">
              <img
                width="300px"
                v-if="episode.image != null"
                class="transform hover:scale-125 duration-500"
                v-bind:src="episode.image.medium"
              />
              <img v-else v-bind:alt="episode.url" />
            </div>
          </div>

          <!-- Summary -->
          <div class="accordion-body text-dark" v-html="episode.summary"></div>

          <!-- Details  -->
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
        </div>
      </div>
    </div>
    <div v-else>
      <h1 style="font-size: 50px">No Episodes To Display</h1>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    episodes: Array,
  },
};
</script>
