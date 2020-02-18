<template>
  <div id="app">
    <donate />
  </div>
</template>

<script>
import Donate from './components/donate.vue'

export default {
  name: 'App',
  components: {
    Donate
  }
}
</script>

<style lang="scss">
body{
  margin: 20px;
  background: #fafbff;
  font-family: 'Poppins', sans-serif;
  *{
    box-sizing: border-box;
  }
  sup{
    line-height: 1;
  }
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
}
</style>
