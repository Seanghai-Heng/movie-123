<template>
  <div>
    <div class="column2 col-span-2 leading-10 ml-4 text-lg">
      <div class="details">
        <ul>
          <li>Movie Name : {{ result.show.name }}</li>
          <li v-if="result.show.rating.average">
            Rating : {{ result.show.rating.average }}
          </li>
          <li v-else>Rating : No Rating</li>
          <li v-if="result.show.schedule.days[0] && result.show.schedule.time">
            Schedule : {{ result.show.schedule.days[0] }} at
            {{ result.show.schedule.time }}
          </li>
          <li v-else>Schdule : Not available</li>
          <li v-if="result.show.runtime">
            Runtime : {{ result.show.runtime }} mns
          </li>
          <li v-else>Runtime : Not available</li>
          <li>Status : {{ result.show.status }}</li>
        </ul>
      </div>
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
