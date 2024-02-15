---
layout: page
title: Academic Journey
permalink: /journey/
description:
---

<head>   
    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
<div class="bg-gradient_solid">
  <div class="container">
    <div class="section-header">
      <h2>My Academic Journey</h2>
      <hr>
    </div>
    <div class="steps">
      <div class="steps-container">
        <div class="content">
          <h2>Lorem ipsum dolor</h2>
          <p>Lorem ipsum dolor sit amet, quo ei simul congue exerci, ad nec admodum perfecto mnesarchum, vim ea mazim fierent detracto. Ea quis iuvaret expetendis his, te elit voluptua dignissim per, habeo iusto primis ea eam.</p>
        </div>
        <i class="step-line"></i>
        <div class="date">2000</div>
      </div>
      <div class="steps-container">
        <div class="content">
          <h2>Lorem ipsum dolor</h2>
          <p>Lorem ipsum dolor sit amet, quo ei simul congue exerci, ad nec admodum perfecto mnesarchum, vim ea mazim fierent detracto. Ea quis iuvaret expetendis his, te elit voluptua dignissim per, habeo iusto primis ea eam.</p>
        </div>
        <i class="step-line"></i>
        <div class="date">2001</div>
      </div>
      <div class="steps-container">
        <div class="content">
          <h2>Lorem ipsum dolor</h2>
          <p>Lorem ipsum dolor sit amet, quo ei simul congue exerci, ad nec admodum perfecto mnesarchum, vim ea mazim fierent detracto. Ea quis iuvaret expetendis his, te elit voluptua dignissim per, habeo iusto primis ea eam.</p>
        </div>
        <i class="step-line"></i>
        <div class="date">2002</div>
      </div>
      <div class="steps-container">
        <div class="content">
          <h2>Lorem ipsum dolor</h2>
          <p>Lorem ipsum dolor sit amet, quo ei simul congue exerci, ad nec admodum perfecto mnesarchum, vim ea mazim fierent detracto. Ea quis iuvaret expetendis his, te elit voluptua dignissim per, habeo iusto primis ea eam.</p>
        </div>
        <i class="step-line"></i>
        <div class="date">2003</div>
      </div>
      <div class="steps-container">
        <div class="content">
          <h2>Lorem ipsum dolor</h2>
          <p>Lorem ipsum dolor.</p>
        </div>
        <i class="step-line"></i>
        <div class="date">2004</div>
      </div>
      <div class="steps-container">
        <div class="content">
          <h2>Start PhD studies</h2>
          <p>Lorem </p>
        </div>
        <i class="step-line"></i>
        <div class="date">2014</div>
      </div>
    </div>
  </div>
</div>
</body>

<style>
:root {
  --primary: #37a9e1;
  --primary-gradient: linear-gradient(45deg, #153c7e 0%, #37a9e1 100%);
}
.section-header {
  text-align: center;
}
.section-header h2 {
  font-size: 28px;
  font-weight: 700;
  margin-bottom: 16px;
}
.section-header hr {
  border: 1px solid #fff;
  width: 56px;
}
.bg-gradient_solid {
  background: var(--primary-gradient);
  color: #fff;
  padding: 48px 0;
}
.steps {
  position: relative;
  margin-top: 32px;
}
.steps::after {
  content: "";
  position: absolute;
  width: 1px;
  background-color: white;
  opacity: 0.4;
  top: 0;
  bottom: 0;
  left: 50%;
}

.steps .content p {
  color: #676767;
  font-size: 16px;
}

.steps .content h2 {
  font-weight: 600;
  font-size: 16px;
  color: #676767;
}

.steps-container {
  position: relative;
  background-color: inherit;
  width: calc(50% + 32px);
}

.steps-container .content {
  padding: 32px;
  background-color: white;
  position: relative;
  border-radius: 0px 0px 80px 0px;
  box-shadow: 0px 16px 27px rgb(0 11 30 / 10%);
}

.steps .steps-container:nth-child(even) {
  left: calc(50% - 32px);
  flex-direction: row-reverse;
}

.steps-container {
  display: flex;
}

.steps .steps-container .date {
  font-weight: 900;
  font-size: 16px;
  color: #ffffff;
  margin-bottom: 10px;
  width: 62px;
  height: 62px;
  background-color: var(--primary);
  border-radius: 50%;
  flex-shrink: 0;
  align-items: center;
  display: flex;
  justify-content: center;
  z-index: 777;
}

.step-line {
  width: 40px;
  background-color: #fff;
  height: 1px;
  margin-top: 31px;
  opacity: 0.4;
  flex-shrink: 0;
}

@media (max-width: 767px) {
  .steps::after {
    left: 32px;
  }
  .steps-container {
    left: 0;
    flex-direction: row-reverse;
    width: auto;
    margin-bottom: 16px;
  }
  .steps .steps-container:nth-child(even) {
    left: 0;
  }
}
</style>
