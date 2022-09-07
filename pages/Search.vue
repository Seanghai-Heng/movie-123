<template>
  <div class="bg-black">
    <div v-if="results[0]" class="container pb-4 text-white">   
      <div v-for="result in results" :key="result.id" class="grid md:grid-cols-3 mb-4">        
            <div class="column1 col-span-1 mr-4">
               <div class="overflow-hidden" v-if="result.show.image"><router-link :to="`/movies/${result.show.id}`"><img class="transform hover:scale-125 duration-500" v-bind:src="result.show.image.medium" v-bind:alt="result.show.name"></router-link> 
               </div>
         </div>
         <div class="column2 col-span-2 leading-10">
            <div class="details">
                <ul>
                <li>Movie Name : {{result.show.name}}</li>
                <li v-if="result.show.rating.average">Rating : {{result.show.rating.average}}</li>
                <li v-else>Rating : No Rating</li>
                <li v-if="result.show.schedule.days[0]&&result.show.schedule.time">Schedule : {{result.show.schedule.days[0]}} at {{result.show.schedule.time}}</li>
                <li v-else>Schdule : Not available</li>
                <li v-if="result.show.runtime">Runtime : {{result.show.runtime}} mns </li>
                <li v-else>Runtime : Not available</li>
                <li>Status :  {{result.show.status}}</li>
                </ul>              
            </div>
         </div>
      </div>
      
    </div>
    <div v-else class="text-white">
        No Results
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Search",
  data() {
    return {
      tvShow: this.$route.query.tvShow,
      results: []
    };
  },
  mounted() {
    axios
      .get(`https://api.tvmaze.com/search/shows?q=${this.tvShow}`)
      .then(response => {
        (this.results = response.data), console.log(response.data);
      });
  }
};
</script>

<style>
.grid >.column1> img{
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
