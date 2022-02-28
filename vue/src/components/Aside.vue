<template>
<div>
  <el-menu
        style="width:200px; min-height: calc(100vh - 50px);"
        default-active="user"
        default-openeds="[1]"
        class="el-menu-vertical-demo"
      >
        <el-sub-menu index="1">
          <template #title>
            <el-icon><location /></el-icon>
            <span>系统管理</span>
          </template>
          <el-menu-item index="user" :route="{path:'/'}">
            <el-icon><icon-menu /></el-icon>
            <span>会员管理</span>
          </el-menu-item>
          <el-menu-item index="good" :route="{path:'/'}">
            <el-icon><setting /></el-icon>
            <span>商品管理</span>
          </el-menu-item>
        </el-sub-menu>
    </el-menu>
</div>
</template>

<script>
export default {

}
</script>

<style>

</style>