<template>
  <div class="funded">
    <p v-html="funds"></p>
  </div>
</template>

<script>
export default {
  name: 'Funded',
  props: {
    goal: Number,
    donations: Number
  },
  computed: {
    funds () {
      return this.goal > this.donations
        ? '<b><sup>$</sup>' + (this.goal - this.donations).toLocaleString() + '</b> still needed to fund this project'
        : '<b><sup>$</sup>' + (this.donations - this.goal).toLocaleString() + '</b> over the goal of <sup>$</sup>' + this.goal
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .funded{
    position: absolute;
    width: 100%;
    color: #356ae6;
    background:#e4ebfd;
    bottom: calc(100% + 20px);
    padding:10px 15px;
    margin: 0;
    opacity: 0;
    border-radius: 5px;
    animation: slide .5s 1s forwards;
    p{
      margin: 0;
    }
    &:after{
      content: "";
      width: 0; 
      height: 0; 
      border-left: 14px solid transparent;
      border-right: 14px solid transparent;
      border-top: 14px solid #e4ebfd;
      position: absolute;
      bottom: -13px;
      right: 30px;
    }
  }
  @keyframes slide {
    from {opacity: 0; bottom: calc(100% + 40px);}
    to {opacity: 1;bottom:calc(100% + 20px);}
  }
</style>
