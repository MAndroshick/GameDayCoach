<template>
  <div>
    <div class="offense">
      <hr class="red" />
      <div class="crease-top"></div>
      <div class="row">
        <div class="circle">
          <div class="dot"></div>
        </div>
        <div class="circle">
          <div class="dot"></div>
        </div>
      </div>
    </div>
    <hr class="blue" />
    <div class="faceoff">
      <!-- <hr class="red" /> -->
      <img alt="Vue logo" src="@/assets/logo.png" />
    </div>
    <hr class="blue" />
    <div class="defense">
      <div class="row">
        <div class="circle">
          <div class="dot"></div>
        </div>
        <div class="circle">
          <div class="dot"></div>
        </div>
      </div>
      <div class="crease-bottom"></div>
      <hr class="red" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Rink",
};
</script>

<style>
.circle {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: 5px solid red;
  margin: auto;
  position: relative;
}
.dot {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  border: 5px solid red;
  top: 50%;
  left: 50%;
  margin: -10px 0px 0px -10px;
  position: absolute;
}
.crease-bottom {
  height: 100px;
  width: 200px;
  border: 5px solid red;
  border-radius: 150px 150px 0 0;
  margin: auto;
}
.crease-top {
  height: 100px;
  width: 200px;
  border: 5px solid red;
  border-radius: 0 0 150px 150px;
  display: inline-block;
  padding: 0px;
  margin: 0px;
}
img {
  height: 50%;
  width: 50%;
  border-radius: 50%;
  border: 10px solid #fa4616;
  /* border: 10px solid black; */
}
.blue {
  border: solid blue;
}
.red {
  border: solid red;
  /* display: inline-block; */
  margin: -5px;
}
.faceoff,
.offense,
.defense {
  padding-block: 50px;
  text-align: center;
}
</style>
