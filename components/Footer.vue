<template>
  <div>
    <!-- component -->
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/@iconscout/unicons@3.0.6/css/line.css"
    />

    <footer class="bg-black pt-10 pt-10">
      <div
        class="max-w-6xl m-auto text-gray-800 flex flex-wrap justify-between"
      >
        <!-- Col-1 -->
        <div class="p-5 w-1/2 sm:w-4/12 md:w-3/12">
          <!-- Col Title -->
          <div class="text-xs uppercase text-gray-400 font-medium mb-6">
            About us
          </div>

          <!-- Links -->

          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Contact Us
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Visit Us
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Like Us
          </a>
        </div>

        <!-- Col-3 -->
        <div class="p-5 w-1/2 sm:w-4/12 md:w-3/12">
          <!-- Col Title -->
          <div class="text-xs uppercase text-gray-400 font-medium mb-6">
            More information
          </div>

          <!-- Links -->
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            All Movies
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Sitemap
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Booking
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Appointing
          </a>
        </div>

        <!-- Col-3 -->
        <div class="p-5 w-1/2 sm:w-4/12 md:w-3/12">
          <!-- Col Title -->
          <div class="text-xs uppercase text-gray-400 font-medium mb-6">
            Community
          </div>

          <!-- Links -->
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            GitHub
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Discord
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            Twitter
          </a>
          <a
            href="#"
            class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700"
          >
            YouTube
          </a>
        </div>
      </div>

      <!-- Copyright Bar -->
      <div class="pt-2">
        <div
          class="flex pb-5 px-3 m-auto pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl"
        >
          <div class="mt-2">© Copyright 1998-year. All Rights Reserved.</div>

          <!-- Required Unicons (if you want) -->
          <div class="md:flex-auto md:flex-row-reverse mt-2 flex-row flex">
            <a href="#" class="w-6 mx-1">
              <i class="uil uil-facebook-f"></i>
            </a>
            <a href="#" class="w-6 mx-1">
              <i class="uil uil-twitter-alt"></i>
            </a>
            <a href="#" class="w-6 mx-1">
              <i class="uil uil-youtube"></i>
            </a>
            <a href="#" class="w-6 mx-1">
              <i class="uil uil-linkedin"></i>
            </a>
            <a href="#" class="w-6 mx-1">
              <i class="uil uil-instagram"></i>
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      name: "Movie",
    };
  },
};
</script>

<style scoped>
a {
  color: white;
}
</style>
