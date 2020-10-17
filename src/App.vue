<template>
  <div id="app">
    <div class="background-image"></div>
    <div class="header">
      <h1 class="header__title">Todo List App</h1>
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
  line-height: 80px;
  &__title {
    letter-spacing: 6px;
  }
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
</style>
