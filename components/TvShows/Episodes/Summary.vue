<template>
   <div class="accordion-body text-dark" v-html="episode.summary"></div>
</template>

<script>
export default {
  props: {
    episode: Object,
  },
};
</script>
