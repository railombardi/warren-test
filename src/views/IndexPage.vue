<template>
  <div>
    <WrTable  :transactions="transactions" @showTransactionDetails="openTransactionModal"/>
    <WrTransactionsModal :transactionId="selectedTransactionId" v-if="showModal" @close="closeModal"/>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
  components: {
    WrTable: () => import('../components/WrTable.vue'),
    WrTransactionsModal: () => import('../components/WrTransactionsModal.vue')
  },
  data(){
    return{
      transactions: [],
      showModal: false,
      selectedTransactionId: null
    }
  },
  created(){
    this.getTransactions()
  },
  methods:{
    async getTransactions(){
      let request = await Axios.get('https://warren-transactions-api.herokuapp.com/api/transactions')
      this.transactions = request.data
    },
    openTransactionModal(id){
      this.selectedTransactionId = id
      this.showModal = !this.showModal
    },
    closeModal(){
      this.selectedTransactionId = null
      this.showModal = !this.showModal
    }
  }
}

</script>
