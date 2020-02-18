<template>
  <div class="progress">
    <div class="percent" :style="width"></div>
  </div>
</template>

<script>
export default {
  name: 'Prog',
  props: {
    goal: Number,
    donations: Number
  },
  computed: {
    width () {
      return 'width:'+ ((this.donations / this.goal) * 100) + '%;'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .progress{
    background: rgba(79, 208, 170, 0.44);
    width: 100%;
    height: 13px;
    border-top-right-radius: 5px;
    border-top-left-radius: 5px;
    overflow: hidden;
    .percent{
      background:$green;
      height: 100%;
      width: 0%;
      max-width: 100%;
      transition: width 1s ease;
    }
  }
</style>
