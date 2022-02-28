<template>
  <div style="padding: 10px">
    <div style="margin: 10px 0"><!--功能区域-->
      <el-button type="primary" @click="add">新增</el-button>
      <el-button type="primary">导入</el-button>
      <el-button type="primary">导出</el-button>
    </div>
    <div style="margin: 10px 0"><!--搜索区域-->
      <el-input v-model="search" placeholder="请输入关键字" style="width:20%" clearable></el-input>
      <el-button type="primary" style="margin-left: 5px" @click="load">查询</el-button>
    </div>
    <el-table :data="tableData" border stripe style="width: 100%">
    <el-table-column prop="id" label="ID" sortable />
    <el-table-column prop="username" label="用户名"  />
    <el-table-column prop="nickName" label="昵称" />
    <el-table-column prop="age" label="年龄" />
    <el-table-column prop="sex" label="性别" />
    <el-table-column prop="address" label="地址" />
    <el-table-column fixed="right" label="操作" width="100">
      <template #default="scope">
      <el-popconfirm
      confirm-button-text="确认"
      cancel-button-text="不, 谢谢"
      :icon="InfoFilled"
      icon-color="red"
      title="确认删除吗?"
      @confirm="handleDelete(scope.row.id)"
     >
      <template #reference>
        <el-button type="danger" size="small" >删除</el-button>
      </template>
      </el-popconfirm>
      <el-button  style="margin-left:0px;margin-top:2px" type="primary" size="small" @click="handleEdit(scope.row)">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>
  <div class="dialog" style="margin: 10px 0px">
    <!--分页-->
  <el-pagination
      v-model:currentPage="currentPage"
      :page-sizes="[5,10,20]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
    >
    </el-pagination>
    <!--弹窗-->
    <el-dialog
    v-model="dialogVisible"
    title="Tips"
    width="30%"
    >
    <el-form  :model="form" label-width="120px">
      <el-form-item label="用户名">
        <el-input  v-model="form.username"></el-input>
      </el-form-item>
      <el-form-item label="昵称">
        <el-input v-model="form.nickName"></el-input>
      </el-form-item>
      <el-form-item label="年龄">
        <el-input v-model="form.age"></el-input>
      </el-form-item>
      <el-form-item label="性别">
        <el-radio v-model="form.sex" :label="1">男</el-radio>
        <el-radio v-model="form.sex" :label="2">女</el-radio>
      </el-form-item>
      <el-form-item label="地址">
        <el-input style="width:80%" type="textarea" v-model="form.address"></el-input>
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="save"
          >确认</el-button
        >
      </span>
    </template>
  </el-dialog>
    </div>

  </div>
</template>

<script>
import { InfoFilled } from '@element-plus/icons-vue'
import request from "@/utils/request";
import { ElMessage } from 'element-plus'
export default {
  name: 'Home',
  components: {
  },
  data(){
    return {
      form:{},
      dialogVisible:false,
      search:'',
      currentPage: 1,
      pageSize:10,
      total:10,
      tableData:[]
    }
  },
  created() {
    this.load();
  },
  methods:{
    load(){
      request.get("/api/user", {
        params:{
            pageNum:this.currentPage,
            pageSize:this.pageSize,
            search:this.search}
      }).then(res=>{
            console.log(res)
            this.tableData=res.data.records
            this.total=res.data.total
          })
    },
    handleEdit(row){
      this.form=JSON.parse(JSON.stringify(row))
      this.dialogVisible=true
    },
    add(){
    this.dialogVisible=true
    this.form={}
    },
    save(){
      if(this.form.id){
        request.put("/api/user",this.form).then(res=>{
          console.log(res)
          if(res.code==='0'){
            ElMessage({
              message:'更新成功',
              type:'success',
            })
          } else {
            ElMessage({
              message:res.data.message,
              type:"error",
            })
          }
        })
        this.load()
      } else {
        request.post("/api/user",this.form).then(res=>{
        console.log(res)
          if(res.code==='0'){
              ElMessage({
              type:"success",
              message: '新增成功',
            })
          }else {
            ElMessage({
              type:"error",
              message: res.data.msg,
            })
          }
      })
      }
      this.load()
      this.dialogVisible=false
    },
    handleDelete(id){
      request.delete("/api/user/"+id).then(res=>{
        console.log(res)
        if(res.code==='0'){
          ElMessage({
            type:'success',
            message: '删除成功',
          })
        }else {
          ElMessage({
            type:"error",
            message: res.data.msg,
          })
        }
      })
      this.load()
    },
    handleSizeChange(pageSize){
      this.pageSize=pageSize
      this.load()
    },
    handleCurrentChange(pageNum){
      this.pageNum=pageNum
      this.load()
    },
  }
}
</script>
<style>
.dialog .el-input{
  width:80%;
}
</style>
