<template>
  <!--最外层容器-->
  <el-container style="height:100%">
      <!--顶部导航-->
    <el-header style="text-align:right; height:65px;">
      <img src="..\assets\img\4.png" style="padding-top:5px; float:left; width:55px; height:55px">
      <img src="..\assets\img\11.png" style="padding:15px 0 0 5px; float:left; height:35px">
      <span style="padding-right:5px; font-size:15px; color:#22B8EB">上海机构1</span>
      <span style="padding-right:30px; font-size:15px; color:#22B8EB">·丨</span>
      <el-dropdown trigger="click">
        <i class="iconfont icon-iconfontgerenzhongxin" style="margin-right: 15px; color:#22B8EB; "></i>
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
    <!-- </el-aside> -->
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
        <div class='main'>
          <el-tabs v-model="activeName" @tab-click="handleClick">
            <el-tab-pane label="未完成预约" name="first">未完成预约</el-tab-pane>
            <el-tab-pane label="已完成预约" name="second">已完成预约</el-tab-pane>
          </el-tabs>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'HelloWorld',
}
</script>
<script>
  export default {
    data() {
      return {
        activeName: 'first'
      };
    },
    methods: {
      handleClick(tab, event) {
      }
    }
  };
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
  /* 侧栏样式 */
  .el-aside {
    background-color: #ffffff;
    text-align: center;
  }
  /* 主体界面样式 */
  .el-main {
    background-color: #F7F7F7;
    text-align: center;
    padding:15px 15px 15px 15px;
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
  .main{
    background-color: #fff;
    height:100%;
    border: solid 1px #F0F0F0;    
  }

  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
  .el-tabs__item.is-active{
    color:#22B8EB;
  }
  .el-tabs__item{
    padding:0 25px;
    height:40px;
    line-height: 40px;
    font-size:14px;
    font-weight:500;
    color:#555555;
    position:relative;   
  }
  .el-tabs__nav-wrap::after{
    content:"";
    position:absolute;
    left:25px;
    padding-right:80px;
    height:2px;
    background-color: #F0F0F0;
    z-index:1;
  }
</style>
