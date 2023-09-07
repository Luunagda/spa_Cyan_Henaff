<template>
  <div id="app">
    <nav>
      <router-link to="/">Article App</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  background-color: black;
  color: white;
  font-size: xx-large;
}
body{
  margin: 0;
}

nav a {
  font-weight: bold;
  color: #ffffff;
}

nav a.router-link-exact-active {
  color: #ffffff;
  text-decoration: none;
}
</style>

<script>

</script>
```