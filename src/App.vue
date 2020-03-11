<template>

  <div class="app">
    <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="/about">about</router-link>
    </div>
    <router-view />
  </div>

</template>

<style lang="scss" >

@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,800&display=swap');

* {
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
}

</style>
