<template>   
    <!--主体界面-->
    <div class='main'>
        <!--步骤条/返回/下一步按钮-->
        <el-row :gutter="20" style="margin:20px 20px 0 20px;">
            <el-col :span="20">
                <el-steps :active="0" finish-status="success" simple >
                    <el-step title="选择咨询师" ></el-step>
                    <el-step title="选择咨询日期" ></el-step>
                    <el-step title="预约付款" ></el-step>
                </el-steps>
            </el-col>
            <el-col :span="2">
                <el-button style="width:100%; text-align:center;">返回</el-button>
            </el-col>
            <el-col :span="2">
                <el-button type="primary" style="width:100%; text-align:center; padding:12px 12px" @click="nextStep()">下一步</el-button>
            </el-col>
        </el-row>
        <S1cConselor /> 
    </div>
</template>

<script>
export default {
  name: 'ReserveStep',
}
</script>

<script>
  /* 用vue_axios从后台获取数据 */
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  import S1cConselor from './s1_chooseConselor.vue';

  Vue.use(VueAxios, axios)

  var tData = [];
  export default {
    components: {
        S1cConselor,
    },             
    data() {
      return { 
      
      }
      
    },created() {

    },
    methods: {
      /* 标签页变更 */
      nextStep() {
       
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
  /* 步骤条高度 */
  .el-steps--simple{
      height: 16px;
        
  }
  /* 步骤条：已完成 字体与图标颜色 */
  .el-step__title.is-success,.el-step__head.is-success{
      color:#22B8EB;
      border-color:#22B8EB;
      font-weight:500;
  }
  /* 步骤条：进行中 字体与图标颜色 */
  .el-step__title.is-process,.el-step__head.is-process{
      color:#22B8EB;
      border-color:#22B8EB;
      font-weight:700;
  }


</style>