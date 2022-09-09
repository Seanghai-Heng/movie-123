<template>
  <div>
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
  </div>
</template>

<script>
export default {
  props: {
    result: Object,
  },
};
</script>
