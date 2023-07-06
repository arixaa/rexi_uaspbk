<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li>
            <router-link to="/" class="nav-link">
              <i class="fas fa-cloud"></i> Weather
            </router-link>
          </li>
          <li>
            <router-link to="/location" class="nav-link">
              <i class="fas fa-map-marker-alt"></i> Location
            </router-link>
          </li>
          <li>
            <router-link to="/stopwatch" class="nav-link">
              <i class="fas fa-stopwatch"></i> Stopwatch
            </router-link>
          </li>
          <li>
            <router-link to="/tictactoe" class="nav-link">
              <i class="fas fa-gamepad"></i> Tic Tac Toe
            </router-link>
          </li>
          <li>
            <router-link to="/photo" class="nav-link">
              <i class="fas fa-camera"></i> Photo
            </router-link>
          </li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  text-align: center;
}

header {
  background: linear-gradient(to right, #667eea, #764ba2);
  padding: 20px;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

nav li {
  display: inline-block;
  margin-right: 10px;
}

nav a {
  color: #fff;
  text-decoration: none;
  padding: 5px 10px;
  display: flex;
  align-items: center;
}

.nav-link i {
  margin-right: 5px;
}

nav a:hover {
  text-decoration: underline;
}
</style>
