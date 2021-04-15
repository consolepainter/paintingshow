<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">轮播图</router-link> 
      <router-link to="/about">遮罩效果</router-link>
      <router-link to="/logo">SVG案例</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style scoped>
#app {
  position: relative;
  width: 100vw;
  height: 100vh;
  text-align: center;
  color: #2c3e50;
}

#nav {
  position: absolute;
  top: 6%;
  right: 6%;
  display: flex;
  flex-direction: column;
  z-index: 10; 
}

#nav a {
  font-weight: bold;
  color: #b598a1;
}

#nav a.router-link-exact-active {
  color: #4c1f24;
}
</style>
