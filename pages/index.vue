<template>
  <div>
    <navheader />
    <cycling />
    <navfooter />

  </div>
</template>

<script>
import Navheader from "~/components/Navheader.vue";
import Navfooter from "~/components/Navfooter.vue";
import Cycling from "~/components/cycling/Cycling.vue";

export default {
  components: {
    Navheader,
    Navfooter,
    Cycling
  }
};
</script>

<style>
body {
  /* background-image: url("~assets/1.jpg"); */
background: black;
    overflow: hidden;
  /* background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  background-size: cover; */
}
.container {
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
