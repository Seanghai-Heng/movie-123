<template>
  <div class="container pb-4 text-white">
    <CheckIfExist :searchResults="searchResults" :searchText="searchText" />

    <div
      v-for="result in searchResults"
      :key="result.id"
      class="grid md:grid-cols-3 mb-4 items-center"
    >
      <SearchImage :result="result" />
      <SearchDetails :result="result" />
    </div>
    <!-- Horizontal Line -->
    <Horizontal_Line />
  </div>
</template>

<script>
import SearchImage from "../Search/SearchImage.vue";
import SearchDetails from "./SearchDetails.vue";
import CheckIfExist from "./CheckIfExists.vue";
import Horizontal_Line from "../Horizontal_Line.vue";
export default {
  props: {
    searchResults: Array,
    searchText: String,
  },
  components: {
    Horizontal_Line,
    SearchImage,
    SearchDetails,
    CheckIfExist,
  },
};
</script>
