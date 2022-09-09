<template>
  <div class="bg-black">
    <!-- loading component -->
    <Loading v-if="loading"/>
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

                <li v-if="result.rating.average">
                  Rating : {{ result.rating.average }}
                </li>
                <li v-else>Rating : No Rating</li>

                <li v-if="result.schedule && result.schedule.time">
                  Schedule : {{ result.schedule.days[0] }} at
                  {{ result.schedule.time }}
                </li>

                <li v-else>Schdule : Not available</li>

                <li v-if="result.runtime">
                  Runtime : {{ result.runtime }} minutes
                </li>
                <li v-else>Runtime : Not Available</li>

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
        <div
          class="flex pb-5 mx-auto px-3pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
        ></div>

        <!-- Episodes Section -->
        <div
          v-if="episodes.length > 0"
          class="accordion accordion-flush"
          id="accordionFlushExample"
        >
          <h1 class="container pb-4 mt-3" style="font-size: 50px">
            The Episodes
          </h1>
          <div v-for="episode in episodes" class="accordion-item">
            <h2 class="accordion-header" :id="`flush-heading${episode.id}`">
              <button
                style="font-weight: bold"
                class="accordion-button collapsed bg-light text-dark"
                type="button"
                data-bs-toggle="collapse"
                :data-bs-target="`#flush-collapse${episode.id}`"
                aria-expanded="false"
                :aria-controls="`flush-collapse${episode.id}`"
              >
                Season {{ episode.season }} Episode {{ episode.number }}
              </button>
            </h2>
            <div
              :id="`flush-collapse${episode.id}`"
              class="accordion-collapse collapse"
              :aria-labelledby="`flush-heading${episode.id}`"
              data-bs-parent="#accordionFlushExample"
            >
              <!-- Accordion Body -->
              <!-- Image -->
              <div class="accordion-body text-dark">
                <div class="overflow-hidden d-flex justify-evenly items-center">
                  <img
                    width="300px"
                    v-if="episode.image != null"
                    class="transform hover:scale-125 duration-500"
                    v-bind:src="episode.image.medium"
                  />
                  <img v-else v-bind:alt="episode.url" />
                </div>
              </div>

              <!-- Summary -->
              <div
                class="accordion-body text-dark"
                v-html="episode.summary"
              ></div>

              <!-- Details  -->
              <div class="accordion-body text-dark">
                <p>
                  <span class="fw-bold">Episode's Name: </span>
                  {{ episode.name }}
                </p>
                <p>
                  <span class="fw-bold">Episode's Type: </span>
                  {{ episode.type }}
                </p>
                <p>
                  <span class="fw-bold">Air Date: </span> {{ episode.airdate }}
                </p>
                <p>
                  <span class="fw-bold">Run Time: </span>
                  {{ episode.runtime }} minutes
                </p>
                <p>
                  <span class="fw-bold" v-if="episode.rating.average"
                    >Rating: {{ episode.rating.average }}</span
                  >
                  <span class="fw-bold" v-else>Rating: "No Rating"</span>
                </p>
              </div>
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
import Loading from "../../components/Loading.vue"
export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href: "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css",
          integrity:
            "sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC",
          crossorigin: "anonymous",
        },
      ],
      script: [
        {
          src: "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js",
          integrity:
            "sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM",
          crossorigin: "anonymous",
        },
        {
          src: "https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js",
        },
        {
          src: "http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js",
        },
      ],
    };
  },
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
      const response = await axios.get(
        `https://api.tvmaze.com/shows/${this.id}?embed[]=episodes&&embed[]=cast`
      );

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
  components:{
    Loading
  }
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
