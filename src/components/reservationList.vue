<template>   
    <!--主体界面-->
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
                    ||data.visitor_phone.toLowerCase().includes(search_visitor_phone.toLowerCase()))
                &&(!search_status
                    ||data.status.toLowerCase().includes(search_status.toLowerCase()))))"
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
                    width="120">
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
                <el-table-column 
                    width="220" 
                    label="操作" 
                    fixed="right">
                    <template slot-scope="scope">
                    <el-button v-if="scope.row.status!='已关闭'" type="primary" size="small">编辑</el-button>
                    <el-button v-if="scope.row.status!='已关闭'&& scope.row.status!='已完成'" type="danger" size="small">关闭</el-button>
                    </template>
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
        <el-tab-pane label="已完成/已关闭预约" name="second">已完成/已关闭预约</el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
export default {
  name: 'ReservationList',
}
</script>

<script>
  /* 用vue_axios从后台获取数据 */
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  
  Vue.use(VueAxios, axios)

  var tData = [];
  export default {    
    data() {
      return {
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
  /* 页面主体 */ 
  .main{
    background-color: #fff;
    height:99.7%;
    border: solid 1px #F0F0F0;
            
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
    display: inline;
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
    display: inline;
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
    display: inline;
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
  
  /* 起始日期时间选择面板位置*/
  .el-picker-panel, .el-date-range-picker{
    margin-left:230px;
  }
  /* 起始日期时间选择面板上方箭头位置*/
  .el-popper[x-placement^=bottom] .popper__arrow{
    margin-left:-100px;
  }

</style>
