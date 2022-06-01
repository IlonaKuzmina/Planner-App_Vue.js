<template>
  <nav>
    <router-link to="/">Planner</router-link>
    <router-link to="/services">Services</router-link>
  </nav>
  <router-view />
</template>

<style lang="scss">
html {
  background-color: #f6eae8;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #f6eae8;
  margin: 0;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #1e0508;
    padding: 15px;

    &.router-link-exact-active {
      color: #ad8786;
    }
  }
}
</style>
