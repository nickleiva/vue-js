<template>
  <div id="app"> 
    <el-menu
      mode="horizontal"
      background-color="#3498db"
      text-color="#ffffff"
      active-text-color="#ffffff"
    >
      <el-menu-item index="1">
        <router-link :to="{ path: '/'}" class="custom-menu-item">Home</router-link>
      </el-menu-item>
      <el-menu-item index="2">
        <router-link :to="{ path: '/todo-list'}" class="custom-menu-item">Todo List</router-link>
      </el-menu-item>
      <el-menu-item index="3">
        <router-link :to="{ path: '/issue-list'}" class="custom-menu-item">Issues</router-link>
      </el-menu-item>
      <el-menu-item index="4">
        <router-link :to="{ path: '/todos-issue'}" class="custom-menu-item">Todo Issues</router-link>
      </el-menu-item>
    </el-menu>

    <router-view />
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  }
}
</script>

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
</style>
