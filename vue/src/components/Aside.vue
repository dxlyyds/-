<template>
<div>
  <el-menu
        style="width:200px; min-height: calc(100vh - 50px);"
        default-active="2"
        class="el-menu-vertical-demo"
        @open="handleOpen"
        @close="handleClose"
      >
        <el-sub-menu index="1">
          <template #title>
            <el-icon><location /></el-icon>
            <span>选项1</span>
          </template>
        </el-sub-menu>
        <el-menu-item index="2">
          <el-icon><icon-menu /></el-icon>
          <span>选项2</span>
        </el-menu-item>
        <el-menu-item index="4">
          <el-icon><setting /></el-icon>
          <span>选项3</span>
        </el-menu-item>
    </el-menu>
</div>
</template>

<script>
export default {

}
</script>

<style>

</style>