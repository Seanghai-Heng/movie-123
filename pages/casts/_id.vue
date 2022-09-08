<template>
  <div>Cast Page</div>
</template>

<script>
import axios from "axios";
export default {
  name: "TV-Show-Casts",
  data() {
    return {
      id: this.$route.params.id,
      result: [],
      loading: true,
    };
  },
  methods: {
    async showCastInfo() {
      const response = await axios
        .get(`https://api.tvmaze.com/people/${this.id}`)
        .catch(function (error) {
          // console.log(error)
        });
      console.log(response.data);
      this.result = response.data;
      this.loading = false;
    },
  },
  mounted() {
    this.showCastInfo();
  },
};
</script>
