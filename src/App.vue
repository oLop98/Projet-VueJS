<template>
  <nav>
    <router-link to="/">ToDoList</router-link> |
    <router-link to="/AboutView">A propos</router-link>
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #333;
}

nav a.router-link-exact-active {
  color: #3851e1;
}
</style>
