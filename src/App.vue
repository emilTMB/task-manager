<template>
  <div id="app">
    <nav>
      <router-link to="/">Главная</router-link>
    </nav>
    <router-view />
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
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

a {
  text-decoration: none;
}

button {
  margin-left: 10px;
}

li {
  margin-bottom: 15px;
  border-bottom: 1px solid #2c3e50;
}

.container {
  display: block;
  width: 600px;
  margin: 0 auto;
  border: 1px solid #2c3e50;
  border-radius: 15px;
  padding: 15px;
}

button {
  margin-bottom: 15px;
  width: 100px;
}

.task {
  display: flex;
  justify-content: space-between;
}

.next {
  width: 200px;
  height: 50px;
  background-color: #42b983;
  cursor: pointer;
}
.main {
  width: 500px;
  margin: 0 auto;
  border: 1px solid #2c3e50;
  border-radius: 15px;
  padding: 15px;
}

@media screen and (max-width: 768px) {
  .main {
    max-width: 300px;
  }

  .task {
    display: block;
  }

  .container {
    width: 300px;
  }

  li {
    list-style: none;
  }

  ul {
    padding: 0;
  }
}
</style>
