<template>
    <div>
        <!--Step1:选择咨询师 头部-->
        <div style="text-align:left;">
            <span style="color:#373737; font-size:25px;margin-left:25px;">选择咨询师</span>
        </div>
        <!--搜索栏-->
        <div style="float:left;text-align:left;margin:35px 35px 35px 25px">
            <el-form :inline="true" label-width="85px" :label-position="search_form_lable"  class="demo-form-inline" size="medium">{{names}}
                <el-form-item label="咨询师姓名" >
                    <el-select
                        v-model="search_conselor_name"
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
                <el-select style="width:120px" v-model="search_conselor_sex" clearable placeholder="请选择">
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
                <el-form-item label="标签">
                <el-input
                    style="width:120px"
                    v-model="search_conselor_tab"
                    clearable/>  
                </el-form-item>                                                                                                              
            </el-form>
        </div>                                              

        <!--咨询师信息表格-->
        <div style="margin:0 35px 0 25px; height:100%;" >
        <!--搜索栏方法-->
            <el-table
                :data="reserveConselors"
                border
                highlight-current-row
                @current-change="handleCurrentChange"
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
                    label="标签"
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
                      <span  style="margin: 5px 5px 5px 5px"><p style="color:#22B8EB">受训经历：</p><p>{{scope.row.training_experience}}</p></span>
                      <hr style="background-color:#E6E6E6; width:100%; border:none; height:1px; margin-bottom:5px">
                      <span  style="margin: 5px 5px 5px 5px"><p style="color:#22B8EB">资历：</p><p>{{scope.row.seniority}}</p></span>
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
                        :key="reserve_fee"
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
  name: 'S1cConselor',
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
        /* 咨询师按姓名关键字搜索 相关内容初始化 */   
        options: [],
        value: [],
        list: [],
        loading: false,

        /* 其他输入框内容初始化 */
        search_conselor_name:'',
        search_conselor_sex:'',
        search_conselor_tab:'', 
        

        /* step1:选择咨询师 表格初始化 */
        reserveConselors: [] ,                           
      }
      
    },created() {
      /* 获取未完成预约后台信息 */
      this.axios.get('http://106.13.143.112:15000/conselors').then((response) => {
        this.reserveConselors = response.data;
      })
    },
    /* 获取可选择的所有咨询师的姓名 */
    // mounted() {
    //   var names = [];
    //   data.forEach(function(reserveConselors){
    //   names.push({label: item.conselor_name, value: item.conselor_name})
    //   })
    //   this.list = this.names.map(item => {
    //     return { value: item.conselor_name, label: item.conselor_name};
    //   });
    // },
    // data.room.toLowerCase().includes(search_room.toLowerCase()
    methods: {
      remoteMethod(query) {
        if (query !== '') {
          this.loading = true;
          setTimeout(() => {
            this.loading = false;
            this.options = reserveConselors.filter(item => {
              return item.conselor_name.toLowerCase()
                .indexOf(query.toLowerCase()) > -1;
            });
          }, 200);
        } else {
          this.options = [];
        }
      },
      setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row);
      },
      handleCurrentChange(val) {
        this.currentRow = val;
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
