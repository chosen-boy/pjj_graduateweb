<script setup lang="ts">
import {onMounted, reactive} from "vue";
import {  Search } from '@element-plus/icons-vue'
import { ref } from 'vue'
import type { UploadProps, UploadUserFile } from 'element-plus'
const value = ref('')
const fileList = ref<UploadUserFile[]>([

])

const handleChange: UploadProps['onChange'] = (uploadFile, uploadFiles) => {
  fileList.value.push({ name: uploadFile.name });

}
const options = [
  {
    value: '用户1',
    label: '用户1',
  },
  {
    value: '用户2',
    label: '用户2',
  },
  {
    value: '用户3',
    label: '用户3',
  },
  {
    value: '用户4',
    label: '用户4',
  },
  {
    value: '用户5',
    label: '用户5',
  },
]
let status=reactive({
  ishome:true,
  isdata_save:false,
  isdatalist:false
})
onMounted(()=>{

})
function showHome() {
  status.ishome = true;
  status.isdata_save = false;
  status.isdatalist = false;
}
function showdatasave() {
  status.ishome = false;
  status.isdata_save = true;
  status.isdatalist = false;
}
function datalist() {
  status.ishome =false ;
  status.isdata_save = false;
  status.isdatalist = true;
}
function  beforeUpload(file) {
  const isJSON = file.type === 'application/json';
  if (!isJSON) {
    this.$message.error('只能上传 JSON 文件');
    return false; // 阻止上传
  }
  return true; // 允许上传
}


</script>

<template>
  <div class="common-layout screenPage" >
    <el-container >
      <el-header size="large">Header</el-header>
      <el-container>
        <el-aside width="400px">

            <div class="left">
              <el-row class="row-bg" justify="center">
                <el-col :span="20" @click="showHome">首页</el-col>

              </el-row>
              <el-row class="row-bg" justify="center">
                <el-col :span="20" @click="showdatasave">数据储存</el-col>

              </el-row>

            </div>







        </el-aside>
        <el-main class="content_box">
          <div class="home" v-if="status.ishome"> home</div>
          <div class="data_save" v-if="status.isdata_save">
            <div class="user">
              <el-row :gutter="20"> <el-col :span="24" style="font-size: 25px">数据储存</el-col></el-row>
              <el-row :gutter="50">

                <el-col :span="12">
                  <el-select
                    v-model="value"
                    placeholder="Select"
                    size="large"
                    style="width: 240px"
                >
                  <el-option
                      v-for="item in options"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                  />
                </el-select>
                </el-col>
                <el-col :span="12">
                  <el-upload
                      v-model:file-list="fileList"
                      class="upload-demo"
                      action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
                      accept=".json"
                      :before-upload="beforeUpload"
                      :on-change="handleChange"

                  >
                    <el-button type="primary" style="width: 100%">点击上传json文件</el-button>

                  </el-upload>
                </el-col>
              </el-row>
              <el-row :gutter="20"> <el-col :span="24"><el-button type="primary" :icon="Search" @click="datalist">查看结果</el-button></el-col></el-row>

            </div>
          </div>
          <div class="data_list" v-if="status.isdatalist">
            <div class="title">推荐商品列表</div>
            <div class="data_box">
              <div class="goods">

              </div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div><div></div>
              <div></div>
              <div></div>
              <div></div>
              <div></div>

            </div>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<style scoped>
body {
  width: 100%;
  height: 100%;

  background-size: 100%;
}
.common-layout{width: 100%;height: 100%;}
.screenPage {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  margin: auto;

  height: 100%;

  width: 100%;
  background-size: 100% 100%;}

.el-container{
  width: 100%;
  height: 100%;

}
.el-header{
  width: 100%;
  height: 70px;
  font-size: 25px;
  line-height: 70px;
  text-align: center;
background: cornflowerblue;


}
.el-aside{

}
.left{
  width: 300px;
  height: 400px;
  margin: 0 auto;

  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
.left .el-row{
  width: 100%;
  height: 60px;
  .el-col{
    width: 100%;
    height: 100%;
    color: black;
    line-height: 60px;
    text-align: center;
    font-size: 25px;
    background: #535bf2;
    cursor:pointer;
  }

}
.home,.data_save{
  width: 100%;
  height: 100%;

}
.user{
  width: 100%;
  height: 100%;
  background: azure;
  display: flex;
  flex-direction: column;
  justify-content: start;
  border-radius: 10px;
}
.user .el-row{
  margin-top: 100px;
  width: 100%;
  height: 70px;
  .el-col{height: 100%;}
}
.user .el-button{
 width: 200px;
  height: 100px;
}
.upload-demo{width: 200px;height: 100%;}
.el-upload{width: 100%;height: 50px}
.el-upload .el-button{width: 100%;height: 50px}
.data_list{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;

}
.title{width: 100%;height: 60px;font-size: 25px;text-align: center;line-height: 60px}
.data_box{
  width: 100%;
  height: 740px;
  background: #cda066;
  display: flex;
  flex-wrap: wrap;
}
.data_box>div{
  width: 23%; /* 每行显示4个，所以宽度为25% */
  box-sizing: border-box; /* 让边框和填充不会增加元素的宽度 */
  margin:14px ;
  /* 可根据需要调整 */
  background: blueviolet;
}
</style>