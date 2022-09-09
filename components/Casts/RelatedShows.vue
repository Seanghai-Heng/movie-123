<template>
  <div>
    <h1 class="pb-4" style="font-size: 50px">Also Known For</h1>
    <div class="grid gap-4 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
      <div v-for="(castTvShow, index) in castTvShows">
        <router-link :to="`/tvShows/${castTvShow.id}`">
          <div v-if="castTvRefs[index]" class="pb-3">
            <div
              v-if="castTvRefs[index].image"
              class="overflow-hidden d-flex justify-evenly items-center mb-3"
              style="height: 300px"
            >
              <img
                width="300px"
                class="w-full h-full transform hover:scale-125 duration-500"
                :src="castTvRefs[index].image.medium"
              />
            </div>
            <div
              v-else
              class="overflow-hidden d-flex justify-evenly items-center mb-3"
              style="height: 300px"
            >
              <img v-bind:alt="castTvShow.name" />
            </div>
          </div>
        </router-link>

        <h1 class="text-lg text-center">
          <span class="fw-bold" v-if="castTvRefs[index]">
            {{ castTvRefs[index].name }}
          </span>
          in {{ castTvShow.name }}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    castTvShows: Array,
    castTvRefs: Array,
  },
};
</script>
