<template>
  <div id="app" class='container'>
    <div class='columns'>
      <div class='column is-one-fifth'>
        <img src="./assets/logo.png">
      </div>
    </div>


    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang='scss'>

@import '~bulma/bulma';

#app {
  // font-family: 'Avenir', Helvetica, Arial, sans-serif;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  // color: #2c3e50;
  // margin-top: 60px;
}
</style>
