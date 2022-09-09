<template>
  <div>
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
      <h1 class="mt-2 text-black" v-if="result.country">
        Country : {{ result.country.name }}
      </h1>
      <p class="title" v-if="result.birthday">
        Birthday : {{ result.birthday }}
      </p>
      <p class="text-black" style="padding: 10px" v-if="result.gender">
        Gender : {{ result.gender }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    result: Object,
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
