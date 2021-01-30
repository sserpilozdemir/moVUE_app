<template>
  <div class="navbar">
    <div class="links">
      <router-link to="/">Home</router-link>
      <router-link to="/favorites">Favorites</router-link>
    </div>
  </div>
</template>

<style>
.navbar {
  width: 100%;
  height: 50px;
  background-color: #324354;
  color: #fff;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 10px;
}

.navbar a {
  color: #ccc;
  margin-right: 10px;
  text-decoration: none;
}

.navbar a:hover {
  color: #fff;
}

.navbar a.router-link-active,
.navbar a.router-link-exact-active {
  color: #f5e20c;
}
</style>
