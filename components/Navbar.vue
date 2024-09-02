<template>
  <div>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
      <!-- Container wrapper -->
      <div class="container">
        <!-- Navbar brand -->
        <router-link
          to="/"
          @click="$nuxt.$emit('home', 'home')"
          class="navbar-brand"
        >
          <img
            id="MDB-logo"
            src="https://mdbcdn.b-cdn.net/wp-content/uploads/2018/06/logo-mdb-jquery-small.png"
            alt="MDB Logo"
            draggable="false"
            height="30"
          />
        </router-link>

        <!-- Toggle button -->
        <button
          style="outline: none"
          type="button"
          class="navbar-toggler"
          data-toggle="collapse"
          data-target="#navbarCollapse"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <!-- Collapsible wrapper -->
        <div
          class="collapse navbar-collapse navbar-default"
          id="navbarCollapse"
        >
          <form
            class="d-flex align-items-center w-100 form-search ml-3"
            autocomplete="off"
            @submit.stop.prevent="submit"
          >
            <div class="input-group">
              <input
                type="search"
                placeholder="TV Show"
                name="tvShow"
                v-model="tvShow"
                class="form-control"
                aria-label="Search"
              />
              <button
                type="submit"
                class="text-white ml-3"
                @click="$nuxt.$emit('search', tvShow)"
              >
                <i class="fa fa-search mr-3"></i>
              </button>
            </div>
          </form>

          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link
                to="/about"
                class="nav-link d-flex align-items-center"
                style="outline: none"
              >
                <i class="fa fa-bookmark pe-2 mr-2"></i> About
              </router-link>
            </li>
          </ul>
        </div>
        <!-- Collapsible wrapper -->
      </div>
      <!-- Container wrapper -->
    </nav>
  </div>
</template>

<script>
export default {
  name: "movie",
  data() {
    return {
      tvShow: null,
    };
  },
  methods: {
    submit() {
      this.$router.push("/search?tvShow=" + this.tvShow);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
.navbar-dark .nav-item .nav-link {
  color: #fff;
}

.navbar-dark .nav-item .nav-link:hover {
  background-color: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  border-radius: 0.25rem;
  color: #fff;
}

.fa-li {
  position: relative;
  left: 0;
}
input[type="text"]:focus {
  outline: none;
}
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  padding: 63px 0 0 0;
}
</style>
