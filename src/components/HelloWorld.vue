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
          <!--标签页-->
          <el-tabs v-model="activeName" @tab-click="changerev"> 
            <el-tab-pane label="未完成预约" name="first">
              <!--未完成预约头部-->
              <div style="text-align:left;">
                <span style="color:#373737; font-size:25px;margin-left:25px;">未完成预约</span>
                <span style="color:#7A7B7B; font-size:17px; padding: 18px 5px 20px 5px;">Appointment</span>
                <i class="iconfont icon-jia" style="color:#22B8EB; font-size:25px; padding-left:5px; cursor:pointer;"></i>
              </div>
              <div>
                <el-input
                  v-model="search"
                  id="search_vsname"
                  size="mini"
                  placeholder="输入关键字搜索"/>
              </div>
              <!--未完成预约表格-->
              <div style="margin:80px 35px 0 25px; height:100%">
                <el-table
                    :data="UNFreservation"
                    border
                    >
                    <el-table-column
                      type="index"
                      width="50">
                    </el-table-column>
                    <el-table-column
                      prop="reserve_time"
                      label="咨询时间"
                      width="200">
                    </el-table-column>
                    <el-table-column
                      prop="room"
                      label="咨询室"
                      width="100">
                    </el-table-column>
                    <el-table-column
                      prop="counselor"
                      label="咨询师"
                      width="100">
                    </el-table-column> 
                    <el-table-column
                      prop="entry_pereson"
                      label="助理"
                      width="100">
                    </el-table-column>                                                                                   
                    <el-table-column
                      prop="visitor_name"
                      label="姓名"
                      width="150">
                    </el-table-column>                    
                    <el-table-column
                      prop="visitor_sex"
                      label="性别"
                      width="100">
                    </el-table-column>
                    <el-table-column
                      prop="visitor_phone"
                      label="电话"
                      width="180">
                    </el-table-column>
                    <el-table-column
                      prop="birthday"
                      label="出生日期"
                      width="180">
                    </el-table-column>
                    <el-table-column
                      prop="consult_times"
                      label="咨询次数"
                      width="100">                      
                    </el-table-column>
                    <el-table-column
                      prop="entry_time"
                      label="预约时间"
                      width="180">                      
                    </el-table-column>   
                    <el-table-column label="操作" fixed="right">
                        <el-button
                          class="listbutton"
                          @click="handleDelete(scope.$index, scope.row)">编辑</el-button>                  
                    </el-table-column>                                                                                    
                  </el-table>                                
              </div>
            </el-tab-pane>
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
        /* 进入页面时默认进入未完成预约标签页 */
        activeName: 'first',
        /* 未完成预约列表数据 */
        tableData: [{
          reserve_time: '2016-05-02  16:00~17:00',
          room: '咨询室',
          counselor: '陈七',
          entry_pereson: '琪琪',
          visitor_name: '李四',
          visitor_sex: '男',
          visitor_phone: '13466763626',
          birthday: '1993-09-27',
          consult_times: '2',
          entry_time: '2016-05-02 16:30:27',
        },{
          reserve_time: '2016-05-02  16:00~17:00',
          room: '咨询室',
          counselor: '陈七',
          entry_pereson: '琪琪',
          visitor_name: '王五',
          visitor_sex: '男',
          visitor_phone: '13466763626',
          birthday: '1993-09-27',
          consult_times: '2',
          entry_time: '2016-05-02 16:30:27',
        },{
          reserve_time: '2016-05-02  16:00~17:00',
          room: '咨询室',
          counselor: '陈七',
          entry_pereson: '琪琪',
          visitor_name: '张三',
          visitor_sex: '男',
          visitor_phone: '13466763626',
          birthday: '1993-09-27',
          consult_times: '2',
          entry_time: '2016-05-02 16:30:27',
        }],
        search:''
      }
    },
    methods: {
      handleEdit(index, row) {

      },
      handleDelete(index, row) {

      },
      changerev(tab, event) {

      }
    },
    computed:{
      UNFreservation:function(){
        var search=this.search;
        console.log(search)
        if(search){
          return  this.tableData.filter(function(dataNews){
            console.log(dataNews)
            return Object.keys(dataNews).some(function(key){
              return String(visitor_name[key]).toLowerCase().includes(search_vsname.value.toLowerCase())
            })
          })
        }
        return this.tableData
      }
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
  /* 侧栏样式 */
  .el-aside {
    background-color: #ffffff;
    text-align: center;
  }
  /* 页面主体背景 */
  .el-main {
    background-color: #F7F7F7;
    text-align: center;
    padding:0;
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
  /* 页面主体 */ 
  .main{
    background-color: #fff;
    height:100%;
    border: solid 1px #F0F0F0;
    margin:15px 15px 15px 15px;        
  }

  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
  /* 标签页header */
  .el-tabs__header{
    margin:10px 35px 30px 0;

  }
  /* 标签页文字：未选中时 */
  .el-tabs__item{
    padding:0 20px;
    height:40px;
    left:25px;
    line-height: 40px;
    font-size:14px;
    font-weight:500;
    color:#555555;
    position:relative;   
  }
  /* 标签页文字：hover */
  .el-tabs__item:hover{
    color:#22B8EB;
  }
  /* 标签页文字：选中时 */
  .el-tabs__item.is-active{
    color:#22B8EB;
    left:25px;
  }
  /* 标签页线：激活时底线 */
  .el-tabs__active-bar{
    position: absolute;
    bottom:0;
    left:25px;
    height:2px;
    background-color:#22B8EB;
  }
  /* 标签页线：底线 */
  .el-tabs__nav-wrap::after{
    content:"";
    position:absolute;
    left:25px;
    height:2px;
    background-color: #F0F0F0;
    z-index:1;
  }
  
  .el-table{
    position:relative; 
    overflow:hidden;
    box-sizing:border-box;
    height:100%;
  }  
  .listbutton{
    display: inline-block;
    line-height:1;
    white-space:nowrap;
    cursor:pointer;
    box-sizing: border-box;
    outline: 0;
    margin: 0;
    text-align: center;
    vertical-align: center;
    background-color: #22B8EB;
    color:#fff;
    border: 1px solid #22B8EB;
    margin-left: 5px;
    padding: 7px 15px;
    font-size: 12px;

  }
  .listbutton:hover,.listbutton:focus{
    background-color:#fff;
    color:#22B8EB;
    border: 1px solid #22B8EB;
    display: inline-block;
    line-height:1;
    white-space:nowrap;
    cursor:pointer;
    box-sizing: border-box;
    outline: 0;
    margin: 0;
    text-align: center;
    vertical-align: center;
    margin-left: 5px;
    padding: 7px 15px;
    font-size: 12px;
  }
  .listbutton:active{
    background-color:#fff;
    color:#555555;
    border: 1px solid #555555;
    display: inline-block;
    line-height:1;
    white-space:nowrap;
    cursor:pointer;
    box-sizing: border-box;
    outline: 0;
    margin: 0;
    text-align: center;
    vertical-align: center;
    margin-left: 5px;
    padding: 7px 15px;
    font-size: 12px;
  }

</style>
