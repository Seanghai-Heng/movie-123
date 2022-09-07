<template>

    <div class="bg-black">

        <div v-if="result" class="container pb-4 text-white">

            <div class="grid md:grid-cols-3 mb-4">

                <div class="column1 col-span-1 mr-4">

                    <div class="overflow-hidden" v-if="result.image">
                        <img class="transform hover:scale-125 duration-500" v-bind:src="result.image.medium"
                            v-bind:alt="result.name" />

                    </div>

                </div>

                <div class="column2 col-span-2 leading-10">

                    <div class="details">

                        <ul>

                            <li>Movie Name : {{result.name}}</li>

                            <li v-if="result.rating">Rating : {{result.rating.average}}</li>

                            <li v-else>Rating : No Rating</li>

                            <li v-if="result.schedule &&result.schedule.time">
                                Schedule : {{result.schedule.days[0]}} at
                                {{result.schedule.time}}
                            </li>

                            <li v-else>Schdule : Not available</li>

                            <li v-if="result.runtime">Runtime : {{result.runtime}} mns </li>

                            <li v-else>Runtime : Not available</li>

                            <li>Status : {{result.status}}</li>

                        </ul>

                    </div>

                </div>

            </div>

        </div>

        <div v-else class="text-white"> No Results </div>

    </div>

</template>

<script>
import axios from "axios"; export default {
    name: "movie", data() {
        return {
            id
                : this.$route.params.id, tvShow: this.$route.query.tvShow, result: []
        };
    }, mounted() {
        axios.get(` https://api.tvmaze.com/shows/${this.id}`).then(response => {
            (this.result
                = response.data), console.log(this.result.schedule);
        });
    }
};
</script>

<style>
.grid>.column1>img {
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

