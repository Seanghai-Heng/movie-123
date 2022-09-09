<template>
  <div>
    <div v-if="searchResults.length == 0">
      <h1 class="text-lg">No Result</h1>
    </div>
    <h1 v-else style="font-size: 50px" class="text-center mb-2">
      Result Search For "{{ searchText }}"
    </h1>
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
