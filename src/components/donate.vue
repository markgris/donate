<template>
  <div class="donate">
    <funded :goal="goal" :donations="donations" />
    <prog :goal="goal" :donations="donations" />
    <div class="content">
      <h1>Only {{ days | toWords }} days left to fund this project</h1>
      <p>Join the <span>{{contributions}}</span> other donors who have already supported this project.</p>
      <form class="donate-input" v-on:submit.prevent="donated()">
        <input v-model="amount" placeholder="5" required type="Number" min="5">
        <button>Give Now</button>
      </form>
    </div>
    <div :class="{sent : sent}" class="thanks">Thank you for your donation!</div>
  </div>
</template>

<script>
import Funded from './funded.vue'
import Prog from './progress.vue'
var converter = require('number-to-words');

export default {
  name: 'Donate',
  components: {
    Funded,
    Prog
  },
  data () {
    return {
      goal: 5000,
      donations: 0,
      days: 4,
      contributions: 11,
      amount: '',
      sent: false
    }
  },
  methods: {
    donated: function () {
      this.donations = this.donations + Number(this.amount);
      this.contributions++;
      this.amount = '';
      this.sent = true
    }
  },
  created() {
    var self = this;
    setTimeout(function() {
      self.donations = 3750;
    }, 100)
  },
  filters: {
    toWords: function (value) {
      if (!value) return ''
      return converter.toWords(value);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .donate{
    position: relative;
    display: flex;
    flex-direction: column;
    font-family: 'IBM Plex Sans', sans-serif;
    width: 100%;
    max-width: 420px;
    background: #ffffff;
    color: $black;
    margin-bottom: 10vh;
    box-shadow: 0px 0px 10px -3px rgba(0, 0, 0, .3);
    border-radius: 5px;
    .content{
      padding: 35px;
      h1{
        font-family: 'Poppins', sans-serif;
        margin: 0;
        font-size:24px
      }
      p{
        color: $gray;
        margin: 20px 0 35px;
        span{
          font-weight: 600;
          color: $black;
        }
      }
      .donate-input{
        position: relative;
        display: flex;
        width: 100%;
        height: 55px;
        &:after{
          position: absolute;
          display: flex;
          content: "$";
          height: 100%;
          width: 45px;
          color: $gray;
          align-items: center;
          justify-content: center;
          font-size: 20px;
          font-weight: 400;
          opacity: .5;
        }
        &:hover{
          input{
            border: 2px solid $green;
            border-right: none;
          }
        }
        input{
          width: 100%;
          border-top-left-radius: 5px;
          border-bottom-left-radius: 5px;
          border: 2px solid #e3e3e3;
          border-right: none;
          font-size: 24px;
          padding: 10px 10px 10px 32px;
          font-weight: 600;
          color: $black;
          outline: none;
          transition: all .3s ease;
          &:active, &:focus{
            border: 2px solid $green;
            border-right: none;
          }
        }
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
          -webkit-appearance: none;
          margin: 0;
        }
        input[type=number] {
          -moz-appearance:textfield;
        }
        button{
          color: #ffffff;
          background: $green;
          border: 0;
          width: 110px;
          flex: 0 0 110px;
          font-size: 18px;
          font-weight: 600;
          border-top-right-radius: 5px;
          border-bottom-right-radius: 5px;
          outline: none;
          transition: all .3s ease;
          cursor: pointer;
          &:hover{
            background: $greenH;
          }
        }
      }
    }
    .thanks{
      position: absolute;
      bottom: -40px;
      padding: 0 10px;
      width: 100%;
      color: $green;
      opacity: 0;
      transition: all .4s ease;
      &.sent{
        opacity: 1;
      }
    }
  }
</style>
