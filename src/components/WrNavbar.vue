<template>
  <div class="wr-navbar">
    <img class="wr-navbar-img" :src="require('../assets/warren-logo.png')"/>
    <hr>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import '../assets/scss/breakpoints.scss';

.wr-navbar{
  position: fixed;
  width: 100%;
  height: 66px;
  background: #fff;
  padding: 0;
  z-index: 9998;
  &-img{
    margin-left: 64px;
    width: 60px;
    @include mobile(){
      margin-left: 24px;
    }
  }
  hr{
    width: 100%;
    height: 2px;
    background: #ff1f5e;
    border: none;
    margin: 0;
  }
}
</style>