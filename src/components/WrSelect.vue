<template>
  <div class="wr-select" @blur="open = false">
    <div class="selected" :class="{ open: open }" @click="open = !open">
      <span>{{ $t(selected) }}</span>
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, i) of options"
        :key="i"
        @click="emitInput(option)"
      >
        {{ $t(option) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    options:{
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      selected: 'Status',
      open: false
    };
  },
  methods:{
    emitInput(option) {
      this.selected = option;
      this.open = false;
      if(option != 'Status'){
        this.$emit("input", this.selected);
      }
    },
  }
}
</script>

<style lang="scss" scoped>
.wr-select {
  position: relative;
  width: 150px;
  text-align: left;
  outline: none;
  height: 32px;
  line-height: 47px;
}

.wr-select .selected {
  display: flex;
  align-items: center;
  border-radius: 6px;
  border: 1px solid lightgray;
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
  height: 32px;
}

.wr-select .selected.open {
  border-radius: 6px 6px 0px 0px;
}

.wr-select .selected:after {
  position: absolute;
  content: "";
  top: calc(32px - 50%);
  right: 1em;
  width: 0;
  height: 0;
  border: 5px solid transparent;
  border-color: lightgray transparent transparent transparent;
}

.wr-select .items {
  border-radius: 0px 0px 6px 6px;
  overflow: hidden;
  border-left: 1px solid lightgray;
  border-right: 1px solid lightgray;
  border-bottom: 1px solid lightgray;
  position: absolute;
  background-color: #ffff;
  left: 0;
  right: 0;
  z-index: 1;
}

.wr-select .items div {
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
}

.wr-select .items div:hover {
  background-color: #ececec;
}

.selectHide {
  display: none;
}
</style>