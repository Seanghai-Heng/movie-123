<template>
  <div>
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
  </div>
</template>

<script>
export default {
  props: {
    episode : Object
  },
};
</script>
