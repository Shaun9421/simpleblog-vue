<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/demo">Demo页面</router-link>
    </div>
    <img src="./assets/logo.png"> -->
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  max-width: 1024px;
  margin: 0 auto;
}
</style>
