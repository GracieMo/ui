<template>
    <div>
        <!--Step1:选择咨询师 头部-->
        <div style="text-align:left;">
            <span style="color:#373737; font-size:25px;margin-left:25px;">选择咨询师</span>
            <span style="color:#7A7B7B; font-size:17px; padding: 18px 5px 20px 5px;">ChooseConselor</span>
        </div>
        <!--搜索栏-->
        <div style="float:left;text-align:left;margin:35px 35px 35px 25px">
            <el-form :inline="true" label-width="85px" :label-position="search_form_lable"  class="demo-form-inline" size="medium">
                <el-form-item label="咨询师姓名" >
                    <el-select
                        v-model="value"
                        filterable
                        remote
                        reserve-keyword
                        placeholder="请输入姓名关键字"
                        :remote-method="remoteMethod"
                        :loading="loading">
                        <el-option
                        v-for="item in options"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                </el-form-item>                
                <el-form-item label="性别">
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
    </div>            
</template>



<script>
export default {
  name: 'UnFReservationList',
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
        /* 咨询师按姓名关键字搜索 */   
        options: [],
        value: [],
        list: [],
        loading: false,
        states: ["Alabama", "Alaska", "Arizona",
        "Arkansas", "California", "Colorado",
        "Connecticut", "Delaware", "Florida",
        "Georgia", "Hawaii", "Idaho", "Illinois",
        "Indiana", "Iowa", "Kansas", "Kentucky",
        "Louisiana", "Maine", "Maryland",
        "Massachusetts", "Michigan", "Minnesota",
        "Mississippi", "Missouri", "Montana",
        "Nebraska", "Nevada", "New Hampshire",
        "New Jersey", "New Mexico", "New York",
        "North Carolina", "North Dakota", "Ohio",
        "Oklahoma", "Oregon", "Pennsylvania",
        "Rhode Island", "South Carolina",
        "South Dakota", "Tennessee", "Texas",
        "Utah", "Vermont", "Virginia",
        "Washington", "West Virginia", "Wisconsin",
        "Wyoming"],

        /* 其他输入框内容初始化 */
        search_form_lable:'right',
        search_room:'',
        search_conselor:'',
        search_entry_pereson:'',
        search_visitor_name:'',
        search_visitor_phone:'', 
        search_reservetime:'',
        search_status:'',   
        

        /* 未完成预约列表数据 */
        UNFreservation: [] ,                           
      }
      
    },created() {
      /* 获取未完成预约后台信息 */
      this.axios.get('http://106.13.143.112:15000/unFReservationList').then((response) => {
        this.UNFreservation = response.data;
      })
    },
    /* 获取未完成预约后台信息 */
    mounted() {
      this.list = this.states.map(item => {
        return { value: item, label: item };
      });
    },    
    methods: {
      remoteMethod(query) {
        if (query !== '') {
          this.loading = true;
          setTimeout(() => {
            this.loading = false;
            this.options = this.list.filter(item => {
              return item.label.toLowerCase()
                .indexOf(query.toLowerCase()) > -1;
            });
          }, 200);
        } else {
          this.options = [];
        }
      }
    }  
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
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
