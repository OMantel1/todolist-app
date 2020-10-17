<template>
  <div id="app">
    <div class="background-image"></div>
    <div class="header">
      <h1 class="header__title">To Do List</h1>
      <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </nav>
    </div>
    <router-view />
  </div>
</template>


<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
.header {
  text-align: center;
  position: relative;
  top: 0;
  color: white;
  height: 150px;
  width: 100%;
  margin-bottom: 24px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  &__title {
    letter-spacing: 6px;
  }
  a {
    color: black;
    text-decoration: none;
    &.router-link-exact-active {
      color: white;
      font-weight: bold;
      text-decoration: underline;
    }
  }
}

.background-image {
  width: 100%;
  height: 150px;
  position: absolute;
  background-color: rgb(138, 138, 138);
  background-image: url("./assets/notepad-3693309_1920.jpg");
  background-size: cover;
  background-position: 50% 60%;
  filter: blur(1px);
  -webkit-filter: blur(8px);
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 14px;
  color: #2c3e50;
  width: 100%;
  box-sizing: border-box;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
