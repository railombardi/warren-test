<template>
  <div class="index-page">
    <div class="index-page-inputs">
      <WrInput placeholder="Pesquise pelo título" @input="inputSearch = $event"/>
      <WrSelect @input="statusFilter = $event" :options="statusList"/>
    </div>
    <WrTransactionsTable :filterByStatus="statusFilter" :searchValue="inputSearch"  :transactions="transactions" @showTransactionDetails="openTransactionModal"/>
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
    WrExtract: () => import('../components/WrExtract.vue'),
    WrInput: () => import('../components/WrInput.vue'),
    WrSelect: () => import('../components/WrSelect.vue')
  },
  data(){
    return{
      transactions: [],
      showModal: false,
      selectedTransaction: null,
      inputSearch: null,
      statusFilter: null
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
<style lang="scss" scoped>
@import '../assets/scss/breakpoints.scss';

.index-page{
  padding: 24px 64px;
  @include mobile(){
    padding: 24px 0;
  }
  &-inputs{
    display: flex;
    padding-bottom: 24px;
    column-gap: 32px;
    @include mobile(){
      justify-content: center;
    }
  }
}
</style>