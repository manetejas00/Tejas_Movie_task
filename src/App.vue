<template>
  <main>
    <router-view />
  </main>
</template>
<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.vue-bg {
  background: #bce5d0;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
   font-family: poppins;
    background-color: rgba(151,151,151,0.03);

  &::selection {
    background: transparentize(#42B883, 0.5);
  }
}

body {
   margin:0px;
    padding: 0px;
    font-family: poppins;
    background-color: rgba(151,151,151,0.03);
    }

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2C3D4E;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);

  h1 {
    color: #FFF;
    font-size: 28px;

    span {
      color: #42B883;
    }
  }
}
</style>