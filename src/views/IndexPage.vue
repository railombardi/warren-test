<template>
  <div>
    <div>
      
    </div>
    <WrTransactionsTable  :transactions="transactions" @showTransactionDetails="openTransactionModal"/>
    <WrTransactionsModal v-if="showModal" :title="selectedTransaction.title" @close="closeModal">
      <template>
        <div>
          <WrStepper :steps="statusList" :activeStep="transactionStatus"/>
          <div>
            <WrExtract :title="'Transferindo de'" :description="selectedTransaction.from" :value="selectedTransaction.amount" />
          </div>
          <div>
            <WrExtract :title="'Para'" :description="selectedTransaction.to" :value="selectedTransaction.amount" />
          </div>
        </div>
      </template>
    </WrTransactionsModal>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
  components: {
    WrTransactionsTable: () => import('../components/WrTransactionsTable.vue'),
    WrTransactionsModal: () => import('../components/WrTransactionsModal.vue'),
    WrStepper: () => import('../components/WrStepper.vue'),
    WrExtract: () => import('../components/WrExtract.vue')
  },
  data(){
    return{
      transactions: [],
      showModal: false,
      selectedTransaction: null
    }
  },
  computed:{
    statusList(){
      return [
        'created',
        'processing',
        'processed'
      ]
    },
    transactionStatus(){
      return this.selectedTransaction ? this.selectedTransaction.status : ''
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
    async getTransaction(transactionId){
      let request = await Axios.get(`https://warren-transactions-api.herokuapp.com/api/transactions/${transactionId}`)
      return request.data
    },
    async openTransactionModal(transaction){
      this.selectedTransaction = await this.getTransaction(transaction.id)
      this.showModal = !this.showModal
    },
    closeModal(){
      this.selectedTransactionId = null
      this.showModal = !this.showModal
    }
  }
}

</script>
