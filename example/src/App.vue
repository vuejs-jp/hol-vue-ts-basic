<template>
  <div id="app">
    <el-container>
      <el-aside>
        <el-menu id="nav">
          <el-menu-item>
            <router-link to="/">Home</router-link>
          </el-menu-item>
          <el-menu-item>
            <router-link to="/table">Table</router-link>
          </el-menu-item>
          <el-menu-item>
            <router-link to="/form">Form</router-link>
          </el-menu-item>
          <el-menu-item>
            <router-link to="/translator">Translator</router-link>
          </el-menu-item>
          <el-menu-item>
            <router-link to="/about">About</router-link>
          </el-menu-item>
        </el-menu>
      </el-aside>
      <el-main>
        <router-view />
      </el-main>
    </el-container>
  </div>
</template>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
