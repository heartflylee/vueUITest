<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>


  export default {
    name: 'app',
    components: {
    },
    data () {
      return {}
    }
  }
</script>

<style lang="scss">
  html {
    background-color: #eee;
  }

  html, body, p, input {
    margin: 0px;
    padding: 0px;
  }

  ul {
    list-style: none;
  }

  #app {
    height: 100%;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }

</style>
