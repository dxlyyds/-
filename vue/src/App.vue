<template>
<el-config-provider :locale="locale">
  <div>
    <!--* 头部-->
    <Header></Header>
    <!--主体-->
    <div style ="display: flex">
      <!--侧边栏-->
      <Aside></Aside>
      <!--内容-->
      <router-view style="flex: 1"/>
    </div>
  </div>
</el-config-provider>
</template>
<script>
import { ElConfigProvider } from "element-plus"
import zhCn from "element-plus/lib/locale/lang/zh-cn"
import Header from './components/Header.vue';
import Aside from './components/Aside.vue';
export default{
  name:"Layout",
  components:{
    Header,
    Aside,
    [ElConfigProvider.name]:ElConfigProvider,
  },
  data(){
    return{
      locale:zhCn
    }
  }
}
</script>
<style>

</style>
