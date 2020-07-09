<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default  {
  name:  'App'
}
</script>
<style lang="scss">
  .page-wrapper {
    padding-top: 70px;
  }
  .pagination-container{
    background: #747d8a !important;
    padding: 0 !important;
  }
  .el-date-editor.el-range-editor {
    .el-range-input {
      background-color: unset;
    }
  }
</style>
