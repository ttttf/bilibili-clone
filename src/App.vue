<template>
  <div id="app">
    <keep-alive>
      <router-view v-if="$route.meta.keepalive" />
    </keep-alive>
      <router-view v-if="!$route.meta.keepalive" />
  </div>
</template>

<script>

</script>

<style>
body{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  background-color: #f4f4f4;
  font-family: PingFangSC-Regular
}
h2{
  padding: 0;
  margin: 0;
}
</style>
