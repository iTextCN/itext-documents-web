<style scoped lang="less">
  @import "../static/styles/index.less";
</style>
<style>
  .index-version .ivu-badge-count{
    box-shadow: none;
    right: 0;
    top: -3px;
    color: #f50;
    background: transparent;
  }
</style>
<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
