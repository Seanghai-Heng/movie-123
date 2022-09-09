<template>
  <div>
    <h1 class="pb-4" style="font-size: 50px">The Summary</h1>
    <p v-html="result.summary" class="pb-4"></p>
  </div>
</template>

<script>
export default {
  props: {
    result: Object,
  },
};
</script>
