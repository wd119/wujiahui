<template>
  <div id="app">
    <Home></Home>

  </div>
</template>
<script>
import Home from './wyy'
export default {
  name: 'App',
  components: {
    Home
  }
}
</script>
<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
  background-color: #f5f5f5;
  color: #333;
}
#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
</style>
