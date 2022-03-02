<template>
  <div>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">Título</th>
        <th scope="col">Descrição</th>
        <th scope="col">Status</th>
        <th scope="col">Valor</th>
      </tr>
      </thead>
    <tbody>
      <tr v-for="item in filteredTransactions" :key="item.id">
        <td>{{ item.title }}</td>
        <td>{{ item.description }}</td>
        <td>{{ item.status }}</td>
        <td>{{ item.amount | currency }}</td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
  props: {
    transactions: {
      type: Array,
      default: () => []
    },
    filterByStatus: {
      type: String,
      default: ''
    },
    searchValue: {
      type: String,
      default: '',
    }
  },
  filters: {
    currency(value){
      if (!value) return ''
      return value.toLocaleString("pt-BR", { minimumFractionDigits: 2 , style: 'currency', currency: 'BRL' });
    }
  },
  computed:{
    filteredTransactions(){
      let filtered = this.transactions.slice()
      if(this.searchValue){
        filtered = this.transactions.filter(t => t.title.toUpperCase().includes(this.searchValue.toUpperCase()))
      }
      if(this.filterByStatus){
        filtered = filtered.filter(t => t.status.toUpperCase().includes(this.filterByStatus.toUpperCase()))
      }
      return filtered.sort((a,b) => new Date(b.date) - new Date(a.date)) 
    }
  }
}
</script>

<style lang="scss" scoped>
table{
  border-spacing: 0;
  border: 0.5px solid black;
  thead{
    background: lightgray;
  }
  tr:nth-child(even){
    background: #ececec;
  }
  th, td{
   padding: 10px;
  }
}
</style>
