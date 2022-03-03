<template>
  <div class="wr-modal-mask">
    <div class="wr-modal-wrapper">
      <div class="wr-modal-container">
        <div class="wr-modal-container-header">
          <h2>{{modalTitle}}</h2>
          <WrIconSvg name="close" @click="emitClose"/>
        </div>
        <WrStepper :steps="statusList" :activeStep="transactionStatus"/>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
  components: { 
    WrIconSvg: () => import('./WrIconSvg.vue'),
    WrStepper: () => import('./WrStepper.vue')
  },
  props:{
    transactionId:{
      type: String,
      required: true
    }
  },
  data(){
    return{
      transaction: null
    }
  },
  computed:{
    modalTitle(){
      return this.transaction ? this.transaction.title : ''
    },
    statusList(){
      return [
        'created',
        'processing',
        'processed'
      ]
    },
    transactionStatus(){
      return this.transaction ? this.transaction.status : ''
    }
  },
  created(){
    this.getTransaction()
  },
  methods:{
    async getTransaction(){
      let request = await Axios.get(`https://warren-transactions-api.herokuapp.com/api/transactions/${this.transactionId}`)
      this.transaction = request.data
    },
    emitClose(){
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss" scoped>
.wr-modal {
  &-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(51, 51, 51, 0.6);
    display: table;
    transition: opacity 0.3s ease;
  }
  &-wrapper {
    display: table-cell;
    vertical-align: middle;
    padding: 0 50px;
  }
  &-container {
    background: #ffffff;
    box-shadow: 2px 2px 12px rgba(51, 51, 51, 0.16);
    border-radius: 6px;
    padding: 24px;
    margin: auto;
    width: 800px;
    &-header{
      display: flex;
      justify-content: space-between;
      align-items: center;
      h2{
        margin: 0;
      }
    }
  }
}
</style>