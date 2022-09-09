<template>
  <div class="container pb-4 text-white">
    <div v-if="searchResults.length == 0">
      <h1 class="text-lg">No Result</h1>
    </div>
    <h1 v-else style="font-size: 50px" class="text-center mb-2">
      Result Search For "{{ searchText }}"
    </h1>
    <div
      v-for="result in searchResults"
      :key="result.id"
      class="grid md:grid-cols-3 mb-4 items-center"
    >
      <div class="movie-list p-4">
        <router-link :to="`/tvShows/${result.show.id}`">
          <div
            style="height: 300px"
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
      <div class="column2 col-span-2 leading-10 ml-4 text-lg">
        <div class="details">
          <ul>
            <li>Movie Name : {{ result.show.name }}</li>
            <li v-if="result.show.rating.average">
              Rating : {{ result.show.rating.average }}
            </li>
            <li v-else>Rating : No Rating</li>
            <li
              v-if="result.show.schedule.days[0] && result.show.schedule.time"
            >
              Schedule : {{ result.show.schedule.days[0] }} at
              {{ result.show.schedule.time }}
            </li>
            <li v-else>Schdule : Not available</li>
            <li v-if="result.show.runtime">
              Runtime : {{ result.show.runtime }} mns
            </li>
            <li v-else>Runtime : Not available</li>
            <li>Status : {{ result.show.status }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    searchResults: Array,
    searchText: String,
  },
};
</script>
