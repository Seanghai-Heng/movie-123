<template>
  <div class="bg-black">
    <div v-if="loading" class="text-center">
      <div role="status">
        <svg
          class="inline mr-2 w-8 h-8 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
          viewBox="0 0 100 101"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
            fill="currentColor"
          />

          <path
            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
            fill="currentFill"
          />
        </svg>

        <span class="sr-only">Loading...</span>
      </div>
    </div>

    <div v-else class="container pb-4 text-white">
      <div class="bg-white p-5" v-if="result.length == 0">
        <h1 class="text-black text-center">No Result</h1>
      </div>
      <div v-else>
        <!-- Summary Section -->
        <h1 class="pb-4" style="font-size: 50px">The Summary</h1>
        <p v-html="result.summary" class="pb-4"></p>

        <!-- Image Section -->
        <div class="d-flex justify-center pb-3">
          <div class="column1 col-span-1">
            <div class="overflow-hidden">
              <img
                v-if="result.image"
                width="300px"
                height="300px"
                class="transform hover:scale-125 duration-500"
                v-bind:src="result.image.medium"
                v-bind:alt="result.name"
              />
              <img v-else v-bind:alt="result.name" />
            </div>
          </div>
        </div>
        <!-- Movie Details Section -->
        <div class="d-flex justify-center pb-4">
          <div class="column2 col-span-2 leading-10">
            <div class="details text-lg">
              <ul>
                <li>Movie Name : {{ result.name }}</li>

                <li>Rating : {{ result.rating.average ?? "No Rating" }}</li>

                <li v-if="result.schedule && result.schedule.time">
                  Schedule : {{ result.schedule.days[0] }} at
                  {{ result.schedule.time }}
                </li>

                <li v-else>Schdule : Not available</li>

                <li>Runtime : {{ result.runtime ?? " Not available" }} mns</li>

                <li>Status : {{ result.status }}</li>
              </ul>
            </div>
          </div>
        </div>
        <!-- Casts Section-->
        <div v-if="casts.length > 0">
          <h1 class="container pb-4" style="font-size: 50px">The Casts</h1>
          <div class="grid gap-4 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2">
            <div v-for="cast in casts" class="pb-3">
              <div class="overflow-hidden d-flex justify-evenly items-center">
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
        <div v-else class="container">
          <h1 style="font-size: 50px">No Casts To Display</h1>
        </div>

        <!-- Episodes Section -->
        <div
          v-if="episodes.length > 0"
          id="accordion-collapse"
          data-accordion="collapse"
        >
          <h1 class="container pb-4 mt-3" style="font-size: 50px">
            The Episodes
          </h1>
          <h2 id="accordion-collapse-heading-1">
            <button
              type="button"
              class="flex items-center justify-between w-full p-5 font-medium text-left text-gray-500 border border-b-0 border-gray-200 rounded-t-xl focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
              data-accordion-target="#accordion-collapse-body-1"
              aria-expanded="true"
              aria-controls="accordion-collapse-body-1"
            >
              <span>What is Flowbite?</span>
              <svg
                data-accordion-icon
                class="w-6 h-6 rotate-180 shrink-0"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </button>
          </h2>
          <div
            id="accordion-collapse-body-1"
            class="hidden"
            aria-labelledby="accordion-collapse-heading-1"
          >
            <div
              class="p-5 font-light border border-b-0 border-gray-200 dark:border-gray-700 dark:bg-gray-900"
            >
              <p class="mb-2 text-gray-500 dark:text-gray-400">
                Flowbite is an open-source library of interactive components
                built on top of Tailwind CSS including buttons, dropdowns,
                modals, navbars, and more.
              </p>
              <p class="text-gray-500 dark:text-gray-400">
                Check out this guide to learn how to
                <a
                  href="/docs/getting-started/introduction/"
                  class="text-blue-600 dark:text-blue-500 hover:underline"
                  >get started</a
                >
                and start developing websites even faster with components on top
                of Tailwind CSS.
              </p>
            </div>
          </div>
        </div>
        <div v-else>
          <h1 style="font-size: 50px">No Episodes To Display</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "movie",
  data() {
    return {
      id: this.$route.params.id,
      result: [],
      loading: true,
      casts: [],
      episodes: [],
    };
  },
  methods: {
    async showMovieInfo() {
      const response = await axios
        .get(
          `https://api.tvmaze.com/shows/${this.id}?embed[]=episodes&&embed[]=cast`
        )
        .catch(function (error) {
          // console.log(error)
        });
      console.log(response.data._embedded.episodes);
      this.result = response.data;
      this.casts = response.data._embedded.cast;
      this.episodes = response.data._embedded.episodes;
      this.loading = false;
    },
  },
  mounted() {
    this.showMovieInfo();
  },
};
</script>

<style scoped>
.grid > .column1 > img {
  width: 350px;
  height: 250px;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
