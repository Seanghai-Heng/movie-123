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
  </div>
</template>

<script>
import SearchImage from "../Search/SearchImage.vue";
import SearchDetails from "./SearchDetails.vue";
import CheckIfExist from "./CheckIfExists.vue";
export default {
  props: {
    searchResults: Array,
    searchText: String,
  },
  components: {
    SearchImage,
    SearchDetails,
    CheckIfExist,
  },
};
</script>
