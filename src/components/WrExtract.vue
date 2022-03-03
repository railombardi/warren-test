<template>
  <div class="wr-extract">
    <h3>{{title}}</h3>
    <hr>
    <div class="wr-extract-detail">
      <span>{{description}}</span>
      <span>{{value | currency}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    title:{
      type: String,
      default: ''
    },
    description:{
      type: String,
      default: ''
    },
    value:{
      type: Number,
      default: 0
    }
  },
  filters: {
    currency(value){
      if (!value) return ''
      return value.toLocaleString("pt-BR", { minimumFractionDigits: 2 , style: 'currency', currency: 'BRL' });
    }
  },
}
</script>

<style lang="scss" scoped>
.wr-extract{
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  padding: 20px 0;
  h3{
    text-align: start;
    margin: 0;
  }
  hr{
    width: 100%;
    height: 2px;
    background: #ff1f5e;
    border: none;
  }
  &-detail{
    display: flex;
    justify-content: space-between;
    span{
      font-weight: 500;
    }
  }
}
</style>