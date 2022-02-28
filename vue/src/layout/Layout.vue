<template>
  <div>
    <Header></Header>
  <!--主体-->
    <div style ="display: flex">
    <!--侧边栏-->
      <Aside></Aside>
    <!--内容-->
      <router-view style="flex: 1"/>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header";
import Aside from "@/components/Aside";

import {ElConfigProvider} from "element-plus";

export default {
  name:"Layout",
  components:{
    Header,
    Aside,
    [ElConfigProvider.name]:ElConfigProvider,
  },
}
</script>

<style scoped>

</style>