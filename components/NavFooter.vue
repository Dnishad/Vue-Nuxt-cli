<template>
  <div class="footer">
    <div class="container">
      <p class="footerp">#getbacktocycle</p>
      <p style="float:right">F / T / L</p>  
    </div>
  </div>
</template>
<script>

</script>
<style>
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: transparent;
  color: white;
}
.footerp {
  position: absolute;
  text-transform: uppercase;
  font-weight: 500;
}
.footerp:after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 0.7em;
  border-top: 1px solid white;
  z-index: -1;
  width: 80px;
  margin-left: 150px;
}
</style>

