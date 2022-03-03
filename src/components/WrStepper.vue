<template>
  <ol class="wr-stepper">
    <li v-for="(step, index) in steps" :key="step" :class="isActiveStep(index) ? 'wr-stepper-item active' : 'wr-stepper-item'">
        <h4 class="wr-stepper-title">{{$t(step)}}</h4>
    </li>
</ol>
</template>

<script>
export default {
  props:{
    steps:{
      type: Array,
      default: () => []
    },
    activeStep:{
      type: String,
      default: 'created'
    }
  },
  methods:{
    isActiveStep(stepIndex){
      const activeIndex = this.steps.indexOf(this.activeStep)
      return stepIndex <= activeIndex
    }
  }
}
</script>

<style lang="scss" scoped>
.wr-stepper {
    display: flex;
    flex-wrap: wrap;
}

.wr-stepper-item {
    flex: 1;
    display: flex;
    flex-direction: column;
    text-align: center;
}

.wr-stepper-item.active:before{
    background-color: #ff1f5e;
    border: none;
}
.wr-stepper-item:before {
    size: 3rem;
    content: "";
    position: relative;
    z-index: 1;
    display: block;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    margin: 1rem auto 0;
    border: 1px solid #e0e0e0;
    background: white;
}

.wr-stepper-item.active:not(:first-child):after{
    background-color: #ff1f5e;
}
.wr-stepper-item:not(:first-child):after {
    position: relative;
    top: 24px;
    right: 50%;
    content: "";
    height: 2px;
    background-color: #e0e0e0;
    order: -1;
}
</style>