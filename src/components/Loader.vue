<template>
    <div class="loader-wrapper">
      <span class="loader">
        <span class="loader-inner">
        </span>
      </span>
    </div>
</template>
<script>
import $ from 'jquery'
export default {
  name: 'Loader',
  props: {
    msg: String
  }
}
$(window).on("load",function(){
      $(".loader-wrapper").fadeOut("slow");
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.loader-wrapper {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #242f3f;
  display:flex;
  justify-content: center;
  align-items: center;
}
.loader {
  display: inline-block;
  width: 30px;
  height: 30px;
  position: relative;
  border: 4px solid #Fff;
  animation: loader 2s infinite ease;
}
.loader-inner {
  vertical-align: top;
  display: inline-block;
  width: 100%;
  background-color: #fff;
  animation: loader-inner 2s infinite ease-in;
}
@keyframes loader {
  0% { transform: rotate(0deg);}
  25% { transform: rotate(180deg);}
  50% { transform: rotate(180deg);}
  75% { transform: rotate(360deg);}
  100% { transform: rotate(360deg);}
}
@keyframes loader-inner {
  0% { height: 0%;}
  25% { height: 0%;}
  50% { height: 100%;}
  75% { height: 100%;}
  100% { height: 0%;}
}
</style>
