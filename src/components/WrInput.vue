<template>
  <input :placeholder="placeholder" @input="emitInput"/>
</template>

<script>
export default {
  props:{
    placeholder:{
      type: String,
      default: ''
    }
  },
  data(){
    return{
      inputValue: ''
    }
  },
  methods:{
    emitInput(event){
      this.inputValue = event.target.value
      this.$emit('input', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped>
input{
  width: 150px;
  height: 32px;
  border: 1px solid lightgray;
  border-radius: 15px;
  text-align: center;
}
</style>