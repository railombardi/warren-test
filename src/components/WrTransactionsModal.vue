<template>
  <div class="wr-modal-mask">
    <div class="wr-modal-wrapper">
      <div class="wr-modal-container">
        <div class="wr-modal-container-header">
          <h2>{{title}}</h2>
          <WrIconSvg name="close" @click="emitClose"/>
        </div>
        <div class="wr-modal-container-body">
          <slot/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  components: { 
    WrIconSvg: () => import('./WrIconSvg.vue')
  },
  props:{
    title: {
      type: String,
      default: ''
    }
  },
  methods:{  
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
    margin: auto;
    width: 800px;
    padding: 24px;
    &-header{
      display: flex;
      justify-content: space-between;
      align-items: center;
      h2{
        margin: 0;
      }
    }
    &-body{
      padding: 0 50px;
    }
  }
}
</style>