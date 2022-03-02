<template>
  <div id="app">
    <WrTable  :transactions="transactions"/>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
  name: 'App',
  components: {
    WrTable: () => import('./components/WrTable.vue')
  },
  data(){
    return{
      transactions: []
    }
  },
  created(){
    this.getTransactions()
  },
  methods:{
    async getTransactions(){
      let request = await Axios.get('https://warren-transactions-api.herokuapp.com/api/transactions')
      this.transactions = request.data
    }
  }
}

</script>

<style>
*{
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
