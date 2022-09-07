<template>
  <div>
    <!-- about  -->
    <div id="about" class="about">
      <div class="container">
        <div class="row display_boxflex">
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12">
            <div class="about-box">
              <h2>About Us</h2>
              <p>
                It is a long established fact that a reader will be distracted
                by the readable content of a page when looking at its layout.
                The point of using Lorem Ipsum is that it has a more-or-less
                normal distribution of letters, as opposed to using 'Content
                here, content here', making it look
              </p>
              <a href="Javascript:void(0)">Read More</a>
            </div>
          </div>
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12">
            <div class="about-box">
              <figure><img src="../assets/images/about.png" alt="#" /></figure>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- end abouts -->
  </div>
</template>

<script></script>

<style scoped>
    .display_boxflex {

display: flex;
align-items: center;
flex-wrap: wrap;
}

.about .about-box {
    text-align: left;
    
}
 .about .about-box h2 {
     padding: 0;
     color: #020d0f;
     line-height: 70px;
     font-size: 70px;

 }
 .about .about-box p {
     font-size: 17px;
     line-height: 28px;
     color: #000;
     padding: 35px 0px;
}

 .about .about-box a {
     font-size: 16px;
border: #000 solid 1px;
background-color: #000;
color: #fff;
padding: 9px 0px;
max-width: 171px;
width: 100%;
display: inline-block;
text-align: center;
border-radius: 30px;
 }


 .about .about-box a:hover{ 
     background-color: #0ed1f0;
     border: #0ed1f0 solid 1px;
    color: #fff;
 }
 .about .about-box figure {
     margin: 0;
}
 .about .about-box figure img {
    width: 100%;
}
/* .backgro_mh {background: #0ed1f0; } */
</style>