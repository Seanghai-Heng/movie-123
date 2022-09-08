<template>
  <div class="bg-black pt-4">
    <h2
      style="text-align: center; font-size: 40px; font-weight: bold"
      class="text-white"
    >
      {{ result.name }}
    </h2>

    <div class="card mb-4">
      <div class="overflow-hidden">
        <img
          v-if="result.image != null"
          class="w-full h-full transform hover:scale-125 duration-500"
          v-bind:src="result.image.medium"
        />
        <img v-else v-bind:alt="result.name" />
      </div>
      <h1 class="mt-2" v-if="result.country">Country : {{ result.country.name }}</h1>
      <p class="title" v-if="result.birthday">Birthday : {{ result.birthday }}</p>
      <p style="padding: 10px" v-if="result.gender">Gender : {{ result.gender }}</p>
    </div>
    <div
      class="flex pb-5 mx-auto px-3pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
    ></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href: "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css",
        },
      ],
    };
  },
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

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 300px;
  margin: auto;
  text-align: center;
  font-family: arial;
}

.title {
  color: grey;
  font-size: 18px;
}
</style>
