<template>
  <div id="app">
    <main-comp/>
  </div>
</template>

<script>

import MainComp from './components/MainComp.vue'


export default {
  name: 'app',
  components: {
    MainComp,
  }
}
</script>

<style lang="scss">
  *{
    box-sizing: border-box;
    padding: 0%;
    margin: 0%;
  }

  body{
    width: 100%   
  }
</style>
