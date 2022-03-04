<template>
  <div class="table-wrapper">
    <table class="table" v-if="filteredTransactions.length > 0">
      <thead>
      <tr>
        <th scope="col">Título</th>
        <th scope="col">Descrição</th>
        <th scope="col">Status</th>
        <th scope="col">Valor</th>
      </tr>
      </thead>
    <tbody>
      <tr v-for="item in filteredTransactions" :key="item.id" class="clickable" @click="$emit('showTransactionDetails', item)">
        <td>{{ item.title }}</td>
        <td>{{ item.description }}</td>
        <td>{{ $t(item.status) }}</td>
        <td>{{ item.amount | currency }}</td>
      </tr>
    </tbody>
  </table>
  <h2 v-else>Não há nenhum item correspondente a sua pesquisa</h2>
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
@import '../assets/scss/breakpoints.scss';

.table-wrapper{
  table{
    width: 100%;
    border: 2px solid lightgray;
    border-spacing: 0;
    thead{
      background: lightgray;
    }
    tr{
      &:hover{
        background: lightgray !important;
      }
      &:nth-child(even){
        background: #ececec;
      }
    }
    th, td{
      padding: 15px;
      @include mobile(){
        font-size: 10px;
      }
    }
    .clickable{
      cursor: pointer;
    }
  }
}
</style>
