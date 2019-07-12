<template>
    <div>
        <!--Step2:选择咨询时间 头部-->
        <div style="text-align:left;">
            <span style="color:#373737; font-size:25px;margin-left:25px;">STEP2：选择咨询时间</span>
        </div>
        <!--搜索栏-->
        <div style="float:left;text-align:left;margin:35px 25px 35px 25px">
            <el-form :inline="true" label-width="220px" :label-position="search_form_lable"  class="demo-form-inline" size="medium" style="width:100%">
                <el-form-item label="请选择最多3个您期望的咨询日期"  >
                  <div class="block">
                    <el-date-picker
                      type="dates"
                      v-model="value1"
                      placeholder="选择一个或多个日期"
                      style="width:320px"
                      :picker-options="pickerOptions">
                    </el-date-picker>
                  </div>
                </el-form-item>               
                <el-form-item label="咨询类型" label-width="80px">
                  <el-select style="width:100px" v-model="search_reserve_type" clearable placeholder="请选择">
                      <el-option
                          v-for="item in reservetype"
                          :key="item.value"
                          :label="item.label"
                          :value="item.value">
                      </el-option>
                  </el-select> 
                </el-form-item>
                <el-form-item> 
                  <span v-if="conselorOnSelected != null" style="color:#F56C6C; font-size:20px; font-weight:500px; margin-left:10px;">
                    已选咨询师：{{conselorOnSelected.conselor_name}}
                  </span>
                  <span v-else-if="conselorOnSelected == null" style="color:#F56C6C; font-size:20px; font-weight:500px; margin-left:10px;">
                    未选择咨询师
                  </span>
                </el-form-item>                                                                                                            
            </el-form>
        </div>                                              

        <!--咨询师信息表格-->
        <div style="margin:0 25px 0 25px;" >
        <!--搜索栏方法-->
            <el-table
                :data="reserveConselors.filter(data => (
                (!search_conselor_name
                    ||data.conselor_name.toLowerCase().includes(search_conselor_name.toLowerCase()))
                &&(!search_conselor_sex
                    ||data.conselor_sex.toLowerCase().includes(search_conselor_sex.toLowerCase()))
                &&((search_conselor_tabs.length==0)
                    ||search_conselor_tabs.filter(ctab =>data.tabs.indexOf(ctab) > -1).length==search_conselor_tabs.length)))"
                border
                ref="singleTable"             
                highlight-current-row
                @current-change="handleCurrentChange"
                height="450px"
                >
                <!--step1：选择咨询室 表格主体-->
                <el-table-column
                    type="index"
                    width="50"
                    align="center">                   
                </el-table-column>
                <el-table-column
                    prop="conselor_name"
                    label="姓名"
                    width="150">                    
                </el-table-column>
                <el-table-column
                    prop="conselor_nickname"
                    label="昵称"
                    width="150">
                </el-table-column>
                <el-table-column
                    prop="conselor_sex"
                    label="性别"
                    width="100">
                </el-table-column>                
                <el-table-column
                    label="标签(擅长领域)"
                    width="600">
                    <template slot-scope="scope">
                      <el-tag
                        :key="tab"
                        v-for="tab in scope.row.tabs"
                        style="margin-left: 10px;">
                        {{tab}}
                      </el-tag>
                    </template>                   
                </el-table-column>
                <el-table-column
                  label="受训经历与资历"
                  width="146">
                  <template slot-scope="scope">
                    <el-popover trigger="click" placement="top" width="400">
                      <span  style="margin: 5px 5px 5px 5px"><p style="color:#22B8EB;margin-bottom:5px">受训经历：</p><p>{{scope.row.training_experience}}</p></span>
                      <hr style="background-color:#E6E6E6; width:100%; border:none; height:1px; margin-bottom:5px">
                      <span  style="margin: 5px 5px 5px 5px"><p style="color:#22B8EB;margin-bottom:5px">资历：</p><p>{{scope.row.seniority}}</p></span>
                      <div slot="reference" class="name-wrapper" style="padding: 0 50px 0 50px; ">
                        <i class="iconfont icon-wendang" style="color:#22B8EB; font-size:25px"></i>
                      </div>
                    </el-popover>
                  </template>
                </el-table-column>                  
                <el-table-column
                    label="咨询费用"
                    width="430">
                  <template slot-scope="scope">
                    <span
                        :key="reserve_fee.reserve_type"
                        v-for="reserve_fee in scope.row.reserve_fee"
                        style="margin-left: 20px;">
                        {{ reserve_fee.reserve_type+'：'+reserve_fee.fee+'/次' }}
                    </span>
                  </template>                    
                </el-table-column>                                                                                                                                                                                                                                                  
            </el-table>                                                 
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
        pickerOptions: {              
          disabledDate(time) {
            // 设置可选择的日期为今天之后的一个月内
            let curDate = (new Date()).getTime()
            // 这里算出一个月的毫秒数,这里使用30的平均值,实际中应根据具体的每个月有多少天计算
            let day = 15 * 24 * 3600 * 1000
            let dateRegion = curDate + day
            return time.getTime() < Date.now() || time.getTime() > dateRegion
          }

        },

        /* 其他输入框内容初始化 */
        search_form_lable:'right',
        search_conselor_name:'',
        search_conselor_sex:'',
        search_conselor_tabs:'', 
        

        /* step1:选择咨询师 表格初始化 */
        reserveConselors: [] ,
        /* step1:选择咨询师 标签搜索栏初始化 */
        conselorTabs:[],

        /* 性别下拉框选项 */
        reservetype: [{
          value: '1对1面询',
          label: '1对1面询',
        }, {
          value: '电话咨询',
          label: '电话咨询'
        }],
        value: '', 
        conselorOnSelected:null,                            
      }
    },
    watch: {
      value1: {
        handler(newValue, oldValue) {
          if (newValue != null && newValue.length >= 3) {
            console.log(newValue[0]- 8.64e7+newValue[0]);
            this.pickerOptions.disabledDate=(time)=>{
              return !(time.getTime() == newValue[0].getTime()||time.getTime() == newValue[1].getTime()||time.getTime() == newValue[2].getTime())          
            }
          }else{
            this.pickerOptions.disabledDate=(time)=>{
              let curDate = (new Date()).getTime()
              let day = 15 * 24 * 3600 * 1000
              let dateRegion = curDate + day
              return time.getTime() < Date.now() || time.getTime() > dateRegion
            }            
          }
        }
      }
    },  
    created() {
      /* 获取未完成预约后台信息 */
      this.axios.get('http://106.13.143.112:15000/conselors').then((response) => {
        this.reserveConselors = response.data;
      }),
      /* 获取所有咨询师标签 */
      this.axios.get('http://106.13.143.112:15000/conselors/tabs').then((response) => {
        this.conselorTabs = response.data;
      })      
    },
    methods: {
      /* 表格单选行方法 */
      setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row)           
      },
      handleCurrentChange(val) {
        this.currentRow = val;
        this.conselorOnSelected=this.currentRow;
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

</style>
