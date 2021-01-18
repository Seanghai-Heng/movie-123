<template>
  <div>
<div class="bs-example">
    <nav class="navbar navbar-expand-md navbar-dark">
        <a href="#" class="navbar-brand">Brand</a>
        <button type="button" class="navbar-toggler" data-toggle="collapse" data-target="#navbarCollapse">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse text-white" id="navbarCollapse">
            <div class="navbar-nav">
            <router-link to="/">Home</router-link> 

      <router-link to="/about">About</router-link> 
            </div>
        </div>
        <div class="bg-white shadow flex">
        <input class="input-box rounded p-2 " type="text" placeholder="Try 'Los Angeles'">
        <button class="bg-red-400 hover:bg-red-300 rounded text-white p-2 pl-4 pr-4">
                <p class="font-semibold text-xs">Search</p>
        </button>
    </div>

    </nav>
</div>
  </div>
</template>

<style>
    a{
        margin-right: 20px;
    }
    nav{
        background-color: black !important;
    }
    .input-box{
      border-radius: 100px;
      /* width:30%; */
    }

</style>