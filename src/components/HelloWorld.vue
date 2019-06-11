<template>
  <!--最外层容器-->
  <el-container style="height:100%">
      <!--顶部导航-->
    <el-header style="text-align:right; height:65px;">
      <img src="..\assets\img\4.png" style="padding-top:5px; float:left; width:55px; height:55px">
      <img src="..\assets\img\11.png" style="padding:15px 0 0 5px; float:left; height:35px">
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
                  <el-col :span="5"><div style="color:#555555; font-weight:bold;">{{information.title}}</div></el-col>
                  <el-col :span="6" :offset="13"><div style="text-align:right; color:#FB5252;">{{information.generationDate}}</div></el-col>
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
                <i class="iconfont icon-jia" style="color:#22B8EB; font-size:25px; padding-left:5px; cursor:pointer;" @click="createOreditVisitorFormVisible = true"></i>
              </div>
              <!--搜索栏-->
              <div style="float:left;text-align:left;margin:35px 35px 35px 25px">
                <el-form label-width="85px" :label-position="search_form_lable"  size="medium">
                  <el-form-item label="咨询时间">
                    <el-date-picker
                      v-model="search_reservetime"
                      type="datetimerange"
                      align="right"
                      :picker-options="pickerOptions"
                      start-placeholder="开始日期"
                      end-placeholder="结束日期"
                      :default-time="['8:00:00', '20:00:00']">
                    </el-date-picker>   
                  </el-form-item>               
                </el-form>
                <el-form :inline="true" label-width="85px" :label-position="search_form_lable"  class="demo-form-inline" size="medium">
                  <el-form-item label="咨询室">
                    <el-select style="width:120px" v-model="search_room" clearable placeholder="请选择">
                      <el-option-group 
                        v-for="group in rooms"
                        :key="group.label"
                        :label="group.label">
                        <el-option
                          v-for="item in group.options"
                          :key="item.value"
                          :label="item.label"
                          :value="item.value">
                        </el-option>
                      </el-option-group>
                    </el-select> 
                  </el-form-item>
                  <el-form-item label="咨询师姓名" >
                    <el-input 
                      style="width:120px"
                      v-model="search_conselor"
                      clearable/> 
                  </el-form-item>
                  <el-form-item label="助理姓名">
                    <el-input
                      style="width:120px"
                      v-model="search_entry_pereson"
                      clearable/> 
                  </el-form-item>
                  <el-form-item label="来访者姓名">
                    <el-input
                      style="width:120px"
                      v-model="search_visitor_name"
                      clearable/>  
                  </el-form-item> 
                  <el-form-item label="来访者电话">
                    <el-input
                      style="width:120px"
                      v-model="search_visitor_phone"
                      clearable/>  
                  </el-form-item>
                  <el-form-item label="预约状态">
                    <el-select style="width:120px" v-model="search_status" placeholder="请选择" clearable>
                      <el-option
                        v-for="item in status"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                      </el-option>
                    </el-select>
                  </el-form-item>                                                                                                               
                </el-form>
              </div>                                              

              <!--未完成预约表格-->
              <div style="margin:0 35px 0 25px; height:100%;" >
                <!--搜索栏方法-->
                <el-table
                    :data="UNFreservation.filter(data => (
                    (!search_reservetime 
                    || (new Date(data.reserve_date+' '+data.reserve_time_start).getTime() >= search_reservetime[0].getTime()
                       && new Date(data.reserve_date+' '+data.reserve_time_end).getTime() <= search_reservetime[1].getTime()))              
                    &&(!search_room
                        ||data.room.toLowerCase().includes(search_room.toLowerCase()))
                    &&(!search_visitor_name
                      ||data.visitor_name.toLowerCase().includes(search_visitor_name.toLowerCase()))
                    &&(!search_conselor
                        ||data.conselor.toLowerCase().includes(search_conselor.toLowerCase()))
                    &&(!search_entry_pereson 
                        ||data.entry_pereson.toLowerCase().includes(search_entry_pereson.toLowerCase()))
                    &&(!search_visitor_phone
                        ||data.visitor_phone.toLowerCase().includes(search_visitor_phone.toLowerCase()))))"
                    border
                    :default-sort = "{prop: 'scope', order: 'descending'}"
                    stripe
                    >
                    <!--未完成预约表格主体-->
                    <el-table-column
                      type="index"
                      width="50"
                      align="center">
                    </el-table-column>
                    <el-table-column
                      label="咨询时间"
                      sortable
                      width="250">
                      <template slot-scope="scope">
                        <span style="margin-left: 10px">
                          {{ scope.row.reserve_date+'&nbsp;&nbsp;&nbsp;&nbsp;'+scope.row.reserve_time_start+'~'+scope.row.reserve_time_end }}
                        </span>
                      </template>                      
                    </el-table-column>
                    <el-table-column
                      prop="room"
                      label="咨询室"
                      width="150">
                    </el-table-column>
                    <el-table-column
                      prop="conselor"
                      label="咨询师"
                      width="150">
                    </el-table-column> 
                    <el-table-column
                      prop="entry_pereson"
                      label="助理"
                      width="150">
                    </el-table-column>                                                                                   
                    <el-table-column
                      prop="visitor_name"
                      label="来访者"
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
                      width="150">
                    </el-table-column>
                    <el-table-column
                      prop="status"
                      label="状态"
                      width="100">
                    </el-table-column>                    
                    <el-table-column width="120" label="操作" fixed="right">
                      <template scope="scope">
                        {{scope.row.status}}
                      </template>
                      <!-- <template slot-scope="scope">

                        <el-button v-if:"{{row.status}}='未付款'"
                          class="listbutton"
                          >编辑</el-button>
                        <el-button v-else-if="row.status"
                          class="listbutton"
                          >关闭</el-button>
                        <el-button v-else-if="row.status"
                          class="listbutton"
                          >123</el-button>
                        <el-button v-else-if="row.status"
                          class="listbutton"
                          >000</el-button> 
                      </template>                                                 -->
                    </el-table-column>                                                                                                                         
                  </el-table>                                                 
              </div>
              <el-pagination
                background
                layout="prev, pager, next"
                :total="1000"
                style="float:right; margin-right:25px">
              </el-pagination>              
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
  /* 用vue_axios从后台获取数据 */
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  import Test from './test.vue';
  
  Vue.use(VueAxios, axios)

  var tData = [];
  export default { 
    components: {
      Test,
    },      
    data() {
      return {
        UNRinformation : [],
        msg:[],
        /* 咨询室（沙盘室）下拉列表框选项 */
        rooms: [{
          label: '咨询室',
          options: [{
            value: '咨询室1',
            label: '咨询室1'
          }, {
            value: '咨询室2',
            label: '咨询室2'
          }, {
            value: '咨询室3',
            label: '咨询室3'
          }, {
            value: '咨询室4',
            label: '咨询室4'
          }]
        }, {
          label: '沙盘室',
          options: [{
            value: '沙盘室1',
            label: '沙盘室1'
          }, {
            value: '沙盘室2',
            label: '沙盘室2'
          }],
          value: '',
        }],
        /* 预约状态下拉框选项 */
        status: [{
          value: '未付款',
          label: '未付款'
        }, {
          value: '已付款',
          label: '已付款'
        }, {
          value: '已关闭',
          label: '已关闭'
        }, {
          value: '已完成',
          label: '已完成'
        }],
        value: '',

        /* 其他输入框内容初始化 */
        search_form_lable:'right',
        search_room:'',
        search_conselor:'',
        search_entry_pereson:'',
        search_visitor_name:'',
        search_visitor_phone:'', 
        search_reservetime:'',
        search_status:'',   
        
        /* 进入页面时默认进入未完成预约标签页 */
        activeName: 'first',
        /* 未完成预约列表数据 */
        UNFreservation: [] ,
        /* 咨询时间起止筛选框快捷选项 */
        value1:[],          
        pickerOptions: {           
          shortcuts: [{
            text: '最近一周',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              start.setHours(8);
              start.setMinutes(0);
              start.setSeconds(0);
              end.setHours(20);
              end.setMinutes(0);
              end.setSeconds(0);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近一个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();             
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              start.setHours(8);
              start.setMinutes(0);
              start.setSeconds(0);
              end.setHours(20);
              end.setMinutes(0);
              end.setSeconds(0);               
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近三个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              start.setHours(8);
              start.setMinutes(0);
              start.setSeconds(0);
              end.setHours(20);
              end.setMinutes(0);
              end.setSeconds(0);              
              picker.$emit('pick', [start, end]);
            }
          }]
        },                            
      }
      
    },created() {
      /* 获取未完成预约后台信息 */
      this.axios.get('http://106.13.143.112:15000/').then((response) => {
        this.UNFreservation = response.data;
      }),
      /* 获取未读消息 */
      this.axios.get('http://106.13.143.112:15000/msg/unread').then((response) => {
        this.UNRinformation = response.data;
      })
    },
    methods: {
      /* 编辑方法 */
      handleEdit(index, row) {

      },
      /* 标签页变更 */
      changerev(tab, event) {
       
      },       
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

  /* 侧栏样式 */
  .el-aside {
    background-color: #ffffff;
    text-align: center;
  }
  /* 页面主体背景 */
  .el-main {
    background-color: #F7F7F7;
    text-align: center;
    padding:15px 15px;
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
    height:99.7%;
    border: solid 1px #F0F0F0;
            
  }
  /* 导航包含关系 */
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
    right:35px;
  }
  .el-form-item__label{
    margin:0 0 0 10px;
  }
  /* 表格整体 */
  .el-table{
    position:relative; 
    box-sizing:border-box;
    height:100%;
    font-size:14px;
    top:-25px;
  }
  /* 表格列表操作按钮 */ 
  .listbutton{
    display: inline-block;
    line-height:1;
    white-space:nowrap;
    cursor:pointer;
    box-sizing: border-box;
    outline: 0;
    text-align: center;
    vertical-align: center;
    background-color: #22B8EB;
    color:#fff;
    border: 1px solid #22B8EB;
    margin-left: 0;
    padding: 7px 15px;
    font-size: 12px;

  }
  /* 表格列表操作按钮：hover，focus */ 
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
    text-align: center;
    vertical-align: center;
    margin-left: 0px;
    padding: 7px 15px;
    font-size: 12px;
  }
  /* 表格列表操作按钮：active */ 
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
    text-align: center;
    vertical-align: center;
    margin-left: 0px;
    padding: 7px 15px;
    font-size: 12px;
  }
  /* 搜索栏字体*/ 
  /* .searchfont{
    padding-right:10px;
    font-size:14px;
    display: inline;
  } */
  /* 搜索栏输入框整体*/ 
  /* .el-input{
    position: relative; 
    display: inline;
    width:8%;
    margin:0 20px 0 0;
  } */
  /* 搜索栏输入框*/
  /* .el-input__inner{
    width:8%;
    font-size:12px;
    background-color:#fff;
    border-radius: 4px;
    border:1px solid #DCDFE6;
    box-sizing: border-box;
    color:#606266;
    display: inline;
    height:30px;
    line-height:30px;
    position:relative;       
  } */
  /* 下拉列表框输入框整体*/
  /* .el-select,.el-select>.el-input{
    position: relative;
    display: inline;
    margin:0 15px 0 7px;  
  } */
  /* 下拉列表框输入框*/
  /* .el-select> .el-input__inner{
    width:10%;
    font-size:12px;
    background-color:#fff;
    border-radius: 4px;
    border:1px solid #DCDFE6;
    box-sizing: border-box;
    color:#606266;
    display: inline;
    height:30px;
    line-height:30px;
    position:relative;       
  } */
  /* 下拉列表框下拉面板*/
  /* .el-select-dropdown{
    width:8%;
  } */
  /* 下拉列表框下拉箭头icon*/
  /* .el-input__icon{
    line-height: 20px;
    width:25px;
  } */

  /* 搜索栏label样式*/
  /* .el-form-item__label{
    padding:0 0 0 0;
  } */

  /* 起始日期时间选择框宽度*/
  /* .el-date-editor--datetimerange.el-input, .el-date-editor--datetimerange.el-input__inner{
    width:31%;

  } */
  /* 起始日期时间选择框文字与icon位置*/
  /* .el-date-editor .el-range__icon, .el-date-editor .el-range-separator,.el-date-editor .el-range__close-icon{
    line-height: 20px;
  } */
  /* 起始日期时间选择框文字大小*/
  /* .el-date-editor .el-range-input, .el-date-editor .el-range-separator{
    font-size:12px;
  } */
  /* 起始日期时间选择面板位置*/
  .el-picker-panel, .el-date-range-picker{
    margin-left:230px;
  }
  /* 起始日期时间选择面板上方箭头位置*/
  .el-popper[x-placement^=bottom] .popper__arrow{
    margin-left:-100px;
  }
  /* 起始日期时间选择面板日期时间展示框大小*/
  /* .el-input--small .el-input__inner{
    width:120px;
  } */
  /* 起始日期时间选择面板日期时间展示框位置*/
  /* .el-date-range-picker__time-picker-wrap,.el-date-range-picker__time-picker-wrap{
    padding:0 15px 0 15px;
  } */
</style>
