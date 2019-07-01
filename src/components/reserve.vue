<template>
  <!--最外层容器-->
  <el-container style="height:100%">
      <!--顶部导航-->
    <el-header style="text-align:right; height:65px;">
      <img src="../assets/img/navilogo.png" style="padding-top:5px; float:left; width:55px; height:55px">
      <img src="../assets/img/11.png" style="padding:15px 0 0 5px; float:left; height:35px">
      <span style="padding-right:5px; font-size:15px; color:#22B8EB">上海机构1</span>
      <span style="padding-right:30px; font-size:15px; color:#22B8EB">·丨</span>
      <div class="information">
        <el-badge v-if="UNRinformation.length <= 0" class="dot">
          <el-popover
            placement="bottom"
            width="400"
            trigger="click"
            :visible-arrow="false"> 
            <div>
              <div>
                <el-row>
                  <el-col :span="40" style="margin:5px 5px 5px 5px;">
                    <div style="margin:5px 0 5px 0;">没有未读消息！</div>
                  </el-col>
                </el-row>
                <el-row style="margin:5px 5px 0 5px;">
                  <el-col>
                    <hr style="background-color:#E6E6E6;  width:100%; border:none; height:1px; margin-bottom:5px">
                  </el-col>
                </el-row>                                
              </div>
              <div>
                <el-row style="margin:5px 5px 0 5px;">
                  <el-col :span="5" :offset="19" style="cursor:pointer;">                  
                    <span style="font-size:14px;color:#22B8EB;text-align:right;padding-left:8px;">更多消息</span>
                    <i class="iconfont icon-arrow-" style="padding-left: 5px; color:#22B8EB; font-size:12px;"></i>
                  </el-col>
                </el-row>              
              </div>
            </div>                                 
            <i slot="reference" class="iconfont icon-informatiom" style="cursor:pointer; color:#22B8EB; "></i>                     
          </el-popover>
        </el-badge>
        <el-badge v-else is-dot class="dot">
          <el-popover
            placement="bottom"
            width="400"
            trigger="click"
            :visible-arrow="false"> 
            <div>
              <div v-for="information in UNRinformation" :key="information.id">
                <el-row style="margin:5px 5px 0 5px;">
                  <el-col :span="8">
                    <div v-if="information.title!='预约取消提醒'" style="color:#555555; font-weight:bold;">{{information.title}}</div>
                    <div v-else-if="information.title=='预约取消提醒'" style="color:#F56C6C; font-weight:bold;">{{information.title}}</div>
                  </el-col>
                  <el-col :span="6" :offset="10"><div style="text-align:right; color:#555555;">{{information.generationDate}}</div></el-col>
                </el-row>
                <el-row>
                  <el-col :span="40" style="margin:5px 5px 5px 5px;">
                    <div style="margin:5px 0 5px 0;">{{information.content}}</div>
                  </el-col>
                </el-row>
                <el-row style="margin:5px 5px 0 5px;">
                  <el-col>
                    <hr style="background-color:#E6E6E6;  width:100%; border:none; height:1px; margin-bottom:5px">
                  </el-col>
                </el-row>                                
              </div>
              <div>
                <el-row style="margin:5px 5px 0 5px;">
                  <el-col :span="5" style="cursor:pointer;">
                    <span style="font-size:14px;color:#22B8EB;">一键已读</span>
                    <i class="iconfont icon-dui1" style="padding-left: 5px; color:#22B8EB; font-size:14px;"></i>
                  </el-col>
                  <el-col :span="5" :offset="14" style="cursor:pointer;">                  
                    <span style="font-size:14px;color:#22B8EB;text-align:right;padding-left:8px;">更多消息</span>
                    <i class="iconfont icon-arrow-" style="padding-left: 5px; color:#22B8EB; font-size:12px;"></i>
                  </el-col>
                </el-row>              
              </div>
            </div>                                 
            <i slot="reference" class="iconfont icon-informatiom" style="cursor:pointer; color:#22B8EB; "></i>                     
         </el-popover>   
        </el-badge>
      </div>

      <el-dropdown trigger="click">
        <i class="iconfont icon-iconfontgerenzhongxin" style="cursor:pointer; margin-right: 15px; color:#22B8EB; "></i>
        <el-dropdown-menu slot="dropdown" style="width:240px; margin-top:4px;border:none;padding-bottom:5px; ">
          <el-dropdown-item style="line-height:34px; margin-bottom:5px">
            <i class="iconfont icon-iconfontgerenzhongxin" style="padding-left: 10px; color:#22B8EB"></i>
            <span style="padding-left:10px;font-size:14px;color:#7A7B7B">个人主页</span>
          </el-dropdown-item>
          <el-dropdown-item style="line-height:34px; margin-bottom:5px">
            <i class="iconfont icon-klmxiugaimima" style="padding-left: 10px; color:#22B8EB"></i>
            <span style="padding-left:10px;font-size:14px;color:#7A7B7B">修改密码</span>
          </el-dropdown-item>  
          <hr style="background-color:#E6E6E6; width:100%; border:none; height:1px; margin-bottom:5px">
          <el-dropdown-item style="line-height:34px;">              
            <i class="iconfont icon-tuichu" style="padding-left: 10px; color:#22B8EB"></i>
            <span style="padding-left:10px;font-size:14px;color:#7A7B7B">注销</span>
            </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>        
    </el-header>
    <!--底部容器-->
    <el-container>
    <!--左侧导航-->
      <el-menu default-active="1" class="el-menu-vertical-demo">  
        <el-menu-item index="1">
          <i class="iconfont icon-qianyue" style="font-size:20px; padding-right:20px; padding-left:30px;"></i>
          <span slot="title">预约</span>
        </el-menu-item>
        <el-menu-item index="2">
          <i class="iconfont icon-renshutongji" style="font-size:20px; padding-right:20px; padding-left:30px;"></i>
          <span slot="title">咨询师</span>
        </el-menu-item>
        <el-menu-item index="3">
          <i class="iconfont icon-renshu" style="font-size:20px; padding-right:20px; padding-left:30px;"></i>
          <span slot="title">来访者</span>
        </el-menu-item>
        <el-menu-item index="4">
          <i class="iconfont icon-huiyishi" style="font-size:20px; padding-right:20px; padding-left:30px;"></i>
          <span slot="title">咨询室</span>
        </el-menu-item>                     
      </el-menu>      
      <!--主体界面-->
      <el-main>
        <ReserveStep />
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'Navi',
}
</script>

<script>
  /* 用vue_axios从后台获取数据 */
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  import ReserveStep from './reserveStep.vue'

  Vue.use(VueAxios, axios)
  
  export default {
    components: {
        ReserveStep,
    },           
    data() {
      return {
        /* 初始化未读消息 */  
        UNRinformation : [],
        msg:[],                                  
      }
      
    },created() {
      /* 获取未读消息 */
      this.axios.get('http://106.13.143.112:15000/msg/unread').then((response) => {
        this.UNRinformation = response.data;
      })
    },
    methods: {

    }   
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  /* 顶栏样式 */
  .el-header{
    background-color: #ffffff;
    line-height: 65px;
    border-bottom: solid 1px #F0F0F0;
    padding:0 20px 0 10px;
  }
  /* 未读消息红点样式 */
  .dot {
    margin-right: 40px;
    line-height: 16px;
    margin-bottom:4px;
    color:#FB5252;
  }
  /* 未读消息div整体样式 */
  .information{
    line-height: 65px;
    display: inline-block;
  }


  /* 侧边导航样式：展开后 */
  .el-menu {
    padding-top:15px;
    background-color: #FFFFFF;
    color:#9F9F9F;
    width:200px;
    border-right: solid 1px #F0F0F0; 
  }

  /* 左侧导航：选中后 */ 
  .el-menu-item.is-active {
    background-color: #22B8EB;
    color: #fff;
  }
  /* 左侧导航：未选中时 */ 
  .el-menu-item{
    color: #9F9F9F;
  }
  /* 左侧导航：选中后hover */ 
  .el-menu-item:hover.is-active{
    background-color: #22B8EB;    
    color:#fff;
  }
  /* 左侧导航：未选中时hover */ 
  .el-menu-item:hover{
    background-color: #FFFFFF;
    color:#9F9F9F;
  }
  /* 页面主体背景 */
  .el-main {
    background-color: #F7F7F7;
    text-align: center;
    padding:15px 15px;
  }  
  /* 导航包含关系 */
  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
</style>

