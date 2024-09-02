<template>
  <div>
    <div v-if="searchResults.length == 0">
      <h1 class="text-center text-lg pb-5" style="font-size: 50px">No Result</h1>
    </div>
    <div v-else>
      <h1 style="font-size: 50px" class="text-center mb-2">
        Result Search For "{{ searchText == '' ? '' : searchText }}"
      </h1>
    </div>
  </div>
</template>

<script>
import Horizontal_Line from "../Horizontal_Line.vue";
export default {
  props: {
    searchResults: Array,
    searchText: String,
  },
  components: {
    Horizontal_Line,
  },
};
</script>
