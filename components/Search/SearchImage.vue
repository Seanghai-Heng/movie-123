<template>
  <div>
    <div class="movie-list p-4">
      <router-link :to="`/tvShows/${result.show.id}`">
        <div
          style="height: 300px; width:90%"
          class="movie-poster overflow-hidden d-flex justify-evenly items-center"
        >
          <img
            v-if="result.show.image != null"
            class="w-full h-full transform hover:scale-125 duration-500"
            v-bind:src="result.show.image.medium"
            v-bind:alt="result.show.name"
          />
          <img v-else v-bind:alt="result.show.name" />
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    result : Object
  },
};
</script>
