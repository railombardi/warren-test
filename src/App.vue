<template>
  <div>
    <WrNavbar/>
    <div id="app">
      <IndexPage/>
    </div>
  </div>
</template>

<script>
import WrNavbar from './components/WrNavbar.vue'

export default {
  name: 'App',
  components: {
    WrNavbar,
    IndexPage: () => import('./views/IndexPage.vue')
  },
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 66px;
}
</style>
