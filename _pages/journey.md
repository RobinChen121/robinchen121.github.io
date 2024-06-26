---
layout: page
title:
permalink: /journey/
---

<p style="font-size: 3rem; text-align: center">My Research activities</p>

<body>
  <div class="wrapper">
    <div class="center-line">
      <a href="#" class="scroll-icon"><i class="fa fa-caret-up"></i></a>
    </div>
    <div class="row row-1">
      <section>
        <i class="icon fa fa-heart"></i>
        <div class="details">
          <span class="title" style="margin-left: auto;">Jan, 2024</span>
        </div>
        <p>Start working at Brunel University London as a lecturer in Operations Research & Supply Chain Management</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-2">
      <section>
        <i class="icon fa fa-home"></i>
        <div class="details">
          <span class="title">April, 2023</span>
        </div>
        <p>Attend IMA 2023 in Birmingham, UK</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-1">
      <section>
        <i class="icon fa fa-car"></i>
        <div class="details">
          <span class="title" style="margin-left: auto;">July, 2022</span>
        </div>
        <p>Attend Euro 2022 in Espoo, Finland</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-2">
      <section>
        <i class="icon fa fa-star"></i>
        <div class="details">
          <span class="title">August, 2019</span>
        </div>
        <p>Attend MIM 2019 conference in Berlin, Germany</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-1">
      <section>
        <i class="icon fa fa-rocket"></i>
        <div class="details">
          <span class="title" style="margin-left: auto;">Feb, 2019</span>
        </div>
        <p>Start working at Southwest University, China as a lecturer.</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-2">
      <section>
        <i class="icon fa fa-globe"></i>
        <div class="details">
          <span class="title">July, 2018</span>
        </div>
        <p>Finish PhD studies</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-1">
      <section>
        <i class="icon fa fa-paper-plane"></i>
        <div class="details">
          <span class="title" style="margin-left: auto;">Sep 2016</span>
        </div>
        <p>Attend University of Edinburgh for one year as a visiting PhD student</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
    <div class="row row-2">
      <section>
        <i class="icon fa fa-map-marker-alt"></i>
        <div class="details">
          <span class="title">Sep 2014</span>
        </div>
        <p>Start PhD studies in Beihang University</p>
        <div class="bottom">
          <i></i>
        </div>
      </section>
    </div>
  </div>

</body>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
html{
  scroll-behavior: smooth;
}
body{
  background: 
}
::selection{
  color: #fff;
  background: #3ea0e2;
}
.wrapper{
  max-width: 800px;
  margin: 50px auto;
  padding: 0 20px;
  position: relative;
}
.wrapper .center-line{
  position: absolute;
  height: 100%;
  width: 4px;
  background: #69b8a6;
  left: 50%;
  top: 20px;
  transform: translateX(-50%);
}
.wrapper .row{
  display: flex;
}
.wrapper .row-1{
  justify-content: flex-start;
}
.wrapper .row-2{
  justify-content: flex-end;
}
.wrapper .row section{
  background: 
  border-radius: 5px;
  width: calc(50% - 40px);
  padding: 20px;
  position: relative;
}
.wrapper .row section::before{
  position: absolute;
  content: "";
  height: 15px;
  width: 15px;
  background: #69b8a6;
  top: 28px;
  z-index: -1;
  transform: rotate(45deg);
}
.row-1 section::before{
  right: -7px;
}
.row-2 section::before{
  left: -7px;
}
.row section .icon,
.center-line .scroll-icon{
  position: absolute;
  background: #69b8a6;
  height: 40px;
  width: 40px;
  text-align: center;
  line-height: 40px;
  border-radius: 80%;
  color: #F9E79F;
  font-size: 17px;
  box-shadow: 0 0 0 4px #FEF5E7, inset 0 2px 0 rgba(0,0,0,0.08), 0 3px 0 4px rgba(0,0,0,0.05);
}
.center-line .scroll-icon{
  bottom: 0px;
  left: 50%;
  font-size: 25px;
  transform: translateX(-50%);
}
.row-1 section .icon{
  top: 15px;
  right: -60px;
}
.row-2 section .icon{
  top: 15px;
  left: -60px;
}
.row section .details,
.row section .bottom{
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.row section .details .title{
  font-size: 22px;
  font-weight: 600;
  margin-left: 0;
  margin-right: 0;
}
.row section p{
  margin: 10px 0 17px 0;
}
.row section .bottom a{
  text-decoration: none;
  background: #3ea0e2;
  color: #fff;
  padding: 7px 15px;
  border-radius: 5px;
  /* font-size: 17px; */
  font-weight: 400;
  transition: all 0.3s ease;
}
.row section .bottom a:hover{
  transform: scale(0.97);
}
@media(max-width: 790px){
  .wrapper .center-line{
    left: 40px;
  }
  .wrapper .row{
    margin: 30px 0 3px 60px;
  }
  .wrapper .row section{
    width: 100%;
  }
  .row-1 section::before{
    left: -7px;
  }
  .row-1 section .icon{
    left: -60px;
  }
}
@media(max-width: 440px){
  .wrapper .center-line,
  .row section::before,
  .row section .icon{
    display: none;
  }
  .wrapper .row{
    margin: 10px 0;
  }
}

</style>
