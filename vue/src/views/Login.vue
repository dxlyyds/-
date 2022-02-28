<template>
  <div style="width: 100%; height: 100vh;background-color: darkslateblue;overflow: hidden">
    <div style="width: 450px;margin:100px auto">
      <div style="display:flex; color: #cccccc;font-size: 30px;justify-content:center;align-items:center;padding: 30px;">欢迎登陆</div>
      <el-form ref="form" :model="form" label-width="0px" size="normal">
        <el-form-item>
          <el-input placeholder="请输入用户名" :prefix-icon="Avatar" v-model="form.username">
            <template #prefix>
              <el-icon class="el-input__icon"><avatar /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-input type="password" placeholder="请输入密码" :prefix-icon="More" v-model="form.password">
            <template #prefix>
              <el-icon class="el-input__icon"><More/></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-button v-model="login" type="primary" @click="login">登录</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import { Avatar, More } from '@element-plus/icons-vue'
import request from "@/utils/request";
import {ElMessage} from "element-plus";

export default {
  name: "Login",
  components:{
    Avatar,
    More
  },
  data(){
    return{
      form:{}
    }
  },
  methods:{
    login(){
      request.post("/api/user/login",this.form).then(res=>{
        if(res.code==='0'){
          ElMessage({
            type:"success",
            message:"登录成功"
          })
          this.$router.push("/home")
        }else {
          ElMessage({
            type:"error",
            message:"res.msg"
          })
        }
      })
    }
  }
}
</script>

<style scoped>

</style>