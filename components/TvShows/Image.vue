<template>
  <div>
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
  </div>
</template>

<script>
export default {
  props: {
    result: Object,
  },
};
</script>
