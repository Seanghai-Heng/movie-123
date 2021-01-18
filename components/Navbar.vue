<template>
  <div>
<div class="topnav navbar-dark text-white">
   <router-link to="/">Home</router-link> 
      <router-link to="/about">About</router-link> 
      <router-link to="#">TV Shows</router-link> 
  <div class="search-container">
    <form autocomplete="off">
      <input type="text" placeholder="Search.." name="search">
      <button type="submit"><i class="fa fa-search"></i></button>
    </form>
  </div>
</div>
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

@media screen and (max-width: 600px) {
  .topnav .search-container {
    float: none;
  }
  .topnav a, .topnav input[type=text], .topnav .search-container button {
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
/*     
    .navbar-left{
      width: 70%;
    }
    .navbar-right{
      width:30%;
    }
    a{
        margin-right: 20px;
    }
    a:hover{
      color:white;
      text-decoration: none;
    }
    nav{
        background-color: black !important;
        width:100%;
    }
    .navbar{
      width: 100%;
    }
    input{
      border-radius: 100px;
      
    } */

</style>