<template>
  <div>
    <div class="accordion-body text-dark">
      <div
        class="overflow-hidden d-flex justify-evenly items-center"
        v-if="episode.image"
      >
        <a :href="episode.image.medium" target="_blank">
          <img
            width="300px"
            v-if="episode.image != null"
            class="transform hover:scale-125 duration-500"
            v-bind:src="episode.image.medium"
          />
        </a>
      </div>
      <div v-else class="d-flex justify-evenly items-center">
        <img v-bind:alt="episode.name" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    episode: Object,
  },
};
</script>
