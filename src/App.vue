<template>
  <div id="nav">
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="container-fluid">
        <img height="80" alt="Vue logo" src="./assets/logo.png" />
        <a class="navbar-brand" href="#">CHAT PORTH</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link" to="/">Inicio</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/Chat">Chat</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #232c65;
}

#nav a.router-link-exact-active {
  color: #1b9eb3;
}
.navbar {
  border-radius: 10px;
  background-color: rgb(216, 216, 216);
}
</style>
