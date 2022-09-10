<template>
    <div>
        <div v-if="casts.length > 0">
          <h1 class="container pb-4" style="font-size: 50px">The Casts</h1>
          <div class="grid gap-4 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
            <div v-for="cast in casts" class="pb-3" :key="cast.character.id">
              <div
                class="overflow-hidden d-flex justify-evenly items-center"
                style="height: 300px"
              >
                <router-link :to="`../casts/${cast.person.id}`">
                  <img
                    width="300px"
                    v-if="cast.character.image != null"
                    class="transform hover:scale-125 duration-500"
                    v-bind:src="cast.character.image.medium"
                  />
                  <img v-else v-bind:alt="cast.character.name" />
                </router-link>
              </div>
              <h1 class="text-lg text-center">{{ cast.character.name }}</h1>
            </div>
          </div>
        </div>
        <div v-else class="container pb-4">
          <h1 style="font-size: 50px">No Casts To Display</h1>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      casts: Array,
    },
  };
  </script>
  