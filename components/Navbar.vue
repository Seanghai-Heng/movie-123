<template>
  <div>
<nav class="topnav navbar-dark navbar navbar-expand-sm text-white">
   <button type="button" class="navbar-toggler" data-toggle="collapse" data-target="#navbarCollapse">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse navbar-default" id="navbarCollapse">
   <router-link to="/">Home</router-link> 
      <router-link to="/about">About</router-link> 
      <router-link to="#">TV Shows</router-link> 
      </div>
  <div class="search-container">
    <form autocomplete="off">
      <input type="text" placeholder="Search.." name="search">
      <button type="submit"><i class="fa fa-search"></i></button>
    </form>
  </div>
</nav>
  </div>
</template>

<style>
* {box-sizing: border-box;}

body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

.topnav {
  overflow: hidden;
  background-color: black;
}

.topnav a {
  float: left;
  display: block;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}

.topnav a:hover {
  background-color: #ddd;
  color: black;
}

.topnav a.active {
  background-color: #2196F3;
  color: white;
}

.topnav .search-container {
  float: right;
}

.topnav input[type=text] {
  padding: 6px;
  margin-top: 8px;
  font-size: 17px;
  border: none;
  color: black;
}

.topnav .search-container button {
  float: right;
  padding: 6px 10px;
  margin-top: 8px;
  margin-right: 16px;
  background: black;
  font-size: 17px;
  border: none;
  cursor: pointer;
}
input:focus {
    border: none;
}
.topnav .search-container button:hover {
  background: #ccc;
}

@media screen and (max-width: 680px) {
  .topnav .search-container {
    float: none;
  }
  .navbar-toggler{
    width: 100%;
    text-align: left;
  }
  .search-container{
    width:100%;
  }
  .topnav .search-container button {
    width: 10%;
    text-align: left;
    display:block;
    float: none;
    
  }
  .topnav a{
    padding: 5px;
    margin-right: 20px;
    display: block;
    text-align: left;
    float : none;
    padding:14px;
  }
   .topnav input[type=text]{
    float: none;
    display: block;
    text-align: left;
    width: 100%;
    margin: 0;
    padding: 14px;
  }
  .topnav input[type=text] {
    border: 1px solid #ccc;  
  }
}
</style>