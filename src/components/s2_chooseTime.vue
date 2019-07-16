<template>
    <div>
        <!--Step2:选择咨询时间 头部-->
        <div style="text-align:left;">
            <span style="color:#373737; font-size:25px;margin-left:25px;">STEP2：选择咨询时间</span>
        </div>
        <!--搜索栏-->
        <div style="float:left;text-align:left;margin:35px 25px 20px 25px; width:100%">
            <el-form :inline="true" label-width="220px" :label-position="search_form_lable"  class="demo-form-inline" size="medium">
                <el-form-item label="请选择最多3个您期望的咨询日期"  >
                  <div class="block">
                    <el-date-picker
                      type="dates"
                      v-model="value1"
                      placeholder="选择一个或多个日期"
                      style="width:320px"
                      :picker-options="selectDatepickerOptions">
                    </el-date-picker>
                  </div>
                </el-form-item>               
                <el-form-item label="咨询类型" label-width="80px">
                  <el-select style="width:120px" v-model="search_reserve_type" clearable placeholder="请选择">
                      <el-option
                          v-for="item in reservetypes"
                          :key="item.value"
                          :label="item.label"
                          :value="item.value">
                      </el-option>
                  </el-select> 
                </el-form-item>
                <el-form-item style="width:260px;margin-left:30px">
                  <el-switch
                    style="display: block"
                    v-model="search_reserve_room_type"
                    active-text="需要沙盘室"
                    inactive-text="不需要沙盘室"
                    >
                  </el-switch>
                </el-form-item>
            </el-form>
            <el-form :inline="true" label-width="220px" :label-position="search_form_lable"  class="demo-form-inline" size="medium">
                <el-form-item> 
                  <span v-if="conselorOnSelected != null" style="color:#F56C6C; font-size:20px; font-weight:500px; margin-left:10px;">
                    已选咨询时间：{{conselorOnSelected.conselor_name}}
                  </span>
                  <span v-else-if="conselorOnSelected == null" style="color:#F56C6C; font-size:20px; font-weight:500px; margin-left:10px;">
                    未选择咨询时间
                  </span>
                </el-form-item>                                                                                                                           
            </el-form>
        </div>                                              

        <!--咨询师可预约时间表格-->
        <div style="margin:0 25px 0 25px;float:left;text-align:left;">
          <el-form :inline="true" >
            <el-form-item>
              <el-table
                :data="conselor_available_time"
                height="350"
                border
                style="width:305px"
                ref="singleTable"
                highlight-current-row
                @current-change="selectConselorTimes">
                <el-table-column label="请选择咨询师可预约时间">
                  <el-table-column
                    prop="date"
                    label="日期"
                    width="170">
                  </el-table-column>
                  <el-table-column
                    label="时间"
                    width="130">
                      <template slot-scope="scope">
                      <span>
                          {{ scope.row.time_start+'&nbsp;-&nbsp;'+scope.row.time_end}}
                      </span>
                      </template>                    
                  </el-table-column>
                </el-table-column>
              </el-table>
            </el-form-item>
            <el-form-item>
              <i class="iconfont icon-jiantou-you-cuxiantiao-fill" style="color:#22B8EB; font-size:35px;"></i>
            </el-form-item>
            <el-form-item>   
              <el-table
                :data="room_available_time"
                height="350"
                border
                style="width:280px"
                ref="singleTable"
                highlight-current-row
                @current-change="handleCurrentChange">
                <el-table-column label="请选择咨询室可使用时间">
                  <el-table-column
                    prop="date"
                    label="咨询室/沙盘室"
                    width="150">
                  </el-table-column>
                  <el-table-column
                    label="时间"
                    width="120">
                      <template slot-scope="scope">
                      <span>
                          {{ scope.row.time_start+'&nbsp;-&nbsp;'+scope.row.time_end}}
                      </span>
                      </template>                      
                  </el-table-column>
                </el-table-column>
              </el-table>
          </el-form-item>
            <el-form-item>
              <i class="iconfont icon-jiantou-you-cuxiantiao-fill" style="color:#22B8EB; font-size:35px;"></i>
            </el-form-item>          
          <el-form-item>               
            <el-table
              :data="tableData2"
              height="205"
              border
              style="width:482px">
              <el-table-column label="请确定您的咨询时间">
                <el-table-column
                    prop="reserveDateAndRoomONselected"
                    label="咨询日期与地点"
                    width="202">               
                </el-table-column>
                <el-table-column
                    prop="reserveTime"
                    label="准确咨询时间"
                    width="280">
                    <template slot-scope="scope">
                      <el-time-select
                        style="width:115px"
                        v-model="startTime"
                        :picker-options="{
                          start:scope.row.reserve_available_times_start,
                          end:scope.row.reserve_available_times_end,
                          step: '00:30',
                          maxTime: endTime
                        }">
                      </el-time-select>
                      <span style="margin:0 5px 0 5px">至</span>
                      <el-time-select
                        style="width:115px"
                        v-model="endTime"
                        :picker-options="{
                          start:scope.row.reserve_available_times_start,
                          end:scope.row.reserve_available_times_end,
                          step: '00:30',
                          minTime: startTime
                        }">
                      </el-time-select>
                    </template>                    
                </el-table-column>                
              </el-table-column>
            </el-table>
          </el-form-item>
        </el-form>              
        <!--搜索栏方法-->
                                           
        </div>
    </div>            
</template>



<script>
export default {
  name: 'S2cDate',
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
        /* 多个咨询日期搜索框输入内容 初始化 */
        value1:'',
        /* 多个咨询日期搜索框设置日期选择范围，只可选择从当前日期第二天开始的15天 */
        selectDatepickerOptions: {              
          disabledDate(time) {
            // 设置可选择的日期为今天之后的一个月内
            let curDate = (new Date()).getTime()
            // 这里算出一个月的毫秒数,这里使用30的平均值,实际中应根据具体的每个月有多少天计算
            let day = 15 * 24 * 3600 * 1000
            let dateRegion = curDate + day
            return time.getTime() < Date.now() || time.getTime() > dateRegion
          }
        },

        /* 咨询种类下拉框选项 */
        reservetypes: [{
          value: '1对1面询',
          label: '1对1面询',
        }, {
          value: '电话咨询',
          label: '电话咨询'
        }],
        value: '', 

        /* 其他输入框内容初始化 */
        search_form_lable:'right',
        search_reserve_type:'',
        search_reserve_room_type:false,
        

        /* step2-1:选择咨询师可预约时间 表格初始化 */
        conselor_available_time: [] ,

        /* step2-2:选择咨询室可使用时间 表格初始化 */
        room_available_time: [] ,
        
        /* step2-3:选择具体咨询时间 表格初始化 */
        reserveInfo : [] ,
        tableData2: [{
          reserveDateAndRoomONselected: '2016-05-03 星期二 咨询室3',
          reserve_available_times_start: '9:30',
          reserve_available_times_end: '12:00'
        }],
        startTime: '',
        endTime: '',        

                          
      }
    },
    /* 监听，当多选日期控件选中3个日期后，不可再次选择，若取消已选择的一个日期，可恢复选择 */
    watch: {
      value1: {
        handler(newValue, oldValue) {
          if (newValue != null && newValue.length >= 3) {
            console.log(newValue[0]- 8.64e7+newValue[0]);
            this.selectDatepickerOptions.disabledDate=(time)=>{
              return !(time.getTime() == newValue[0].getTime()||time.getTime() == newValue[1].getTime()||time.getTime() == newValue[2].getTime())          
            }
          }else{
            this.selectDatepickerOptions.disabledDate=(time)=>{
              let curDate = (new Date()).getTime()
              let day = 15 * 24 * 3600 * 1000
              let dateRegion = curDate + day
              return time.getTime() < Date.now() || time.getTime() > dateRegion
            }            
          }
        }
      },
    },  
    created() {
      /* 获取咨询师可预约时间后台信息 */
      this.axios.get('http://106.13.143.112:15000/conselors/2/available/times').then((response) => {
        this.conselor_available_time = response.data;
      }),
      /* 获取咨询室可使用时间后台信息 */
      this.axios.get('http://106.13.143.112:15000/rooms/2/available/times').then((response) => {
        this.room_available_time = response.data;
      })      
    },
    methods: {
      objectSpanMethod({ row, column, rowIndex, columnIndex }) {
        if (columnIndex === 0) {
          if (rowIndex % 2 === 0) {
            return {
              rowspan: 2,
              colspan: 1
            };
          } else {
            return {
              rowspan: 0,
              colspan: 0
            };
          }
        }
      },      
      /* 表格单选行方法 */
      setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row)           
      },
      handleCurrentChange(val) {
        this.currentRow = val;
        this.reserveDateAndRoomONselected=this.currentRow;
        this.$emit('getConselorOnSelected', this.conselorOnSelected)
        return conselorOnSelected;
      },

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
  .el-switch{
    line-height: 36px;
  }
  .el-switch__label{
    vertical-align: baseline;
  }

</style>
