<template>
  <div id="app">
   <IndexPage/>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    IndexPage: () => import('./views/IndexPage.vue')
  },
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
