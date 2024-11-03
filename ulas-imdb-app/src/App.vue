<template>
  <div class="bg-white-100" id="app">
    <nav class="w-full bg-blue-900 text-gray-100">
      <router-link to="/">Home</router-link>
      <router-link to="/favorites">Favorites</router-link>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
}
</script>

<style>
nav {
  display: flex;
  justify-content: center;
  padding: 20px;
  background-color: #f8f9fa;
}

nav a {
  margin: 0 15px;
  text-decoration: none;
}
</style>
