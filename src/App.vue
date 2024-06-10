<template>
  <div id="app">
    <giaoDienChinh />
  </div>
</template>

<script>


import giaoDienChinh from "@/components/giaoDienChinh.vue";

export default {
  name: 'App',
  components: {
    giaoDienChinh
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
  margin-top: 60px;
}
</style>
