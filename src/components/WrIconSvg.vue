<template>
  <div>
    <div
      class="wr-icon-svg"
      @click="emitClick"
    >
      <svg
        v-bind:class="['icon', `icon-${name}`]"
        v-bind:style="{fill: color}"
        viewBox="0 0 100 100"
      >
        <use v-bind:xlink:href="`#icon-${name}`"></use>
      </svg>
    </div>
    <svg display="none" xmlns="http://www.w3.org/2000/svg">
      <symbol id="icon-close" fill="none" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
      <path d="M16.34 9.322a1 1 0 1 0-1.364-1.463l-2.926 2.728L9.322 7.66A1 1 0 0 0 7.86 9.024l2.728 2.926-2.927 2.728a1 1 0 1 0 1.364 1.462l2.926-2.727 2.728 2.926a1 1 0 1 0 1.462-1.363l-2.727-2.926 2.926-2.728z" fill="currentColor"/>
      <path fill-rule="evenodd" clip-rule="evenodd" d="M1 12C1 5.925 5.925 1 12 1s11 4.925 11 11-4.925 11-11 11S1 18.075 1 12zm11 9a9 9 0 1 1 0-18 9 9 0 0 1 0 18z" fill="currentColor"/>
      </symbol>
    </svg>
  </div>
</template>

<script>
export default {
  props:{
    name:{
      type: String,
      required: true
    },
    color:{
      type: String,
      default: ''
    }
  },
  methods: {
    emitClick() {
      this.$emit('click')
    }
  },
}
</script>

<style lang="scss" scoped>
.wr-icon-svg {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer; 

  svg {
    overflow: hidden;
    vertical-align: middle;
    width: 20px;
    height: 20px;
  }
}
</style>