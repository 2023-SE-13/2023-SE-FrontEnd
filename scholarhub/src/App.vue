<template>
  <div id="app">
    <router-view />
    <!-- <HomeView/> -->
  </div>
</template>
<script>
import HomeView from './views/HomeView.vue';
export default {
  name: 'App',
  components: {
    HomeView
  }
}
</script>
<style>
::-webkit-scrollbar{
  display: none;
}
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  /* display: flex; */
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
