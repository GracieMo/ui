<template>   
    <!--主体界面-->
    <div class='main'>
        <!--标签页-->
        <el-tabs v-model="activeName" @tab-click="changerev"> 
          <el-tab-pane label="未完成预约" name="first">
              <UnFReservationList />      
          </el-tab-pane>
          <el-tab-pane label="已完成/已关闭预约" name="second">
              <FocReservationList />
          </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
export default {
  name: 'ReservationTab',
}
</script>

<script>
  /* 用vue_axios从后台获取数据 */
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  import UnFReservationList from './unFReservationList.vue';
  import FocReservationList from './focReservationList.vue'

  Vue.use(VueAxios, axios)

  var tData = [];
  export default {
    components: {
        UnFReservationList,
        FocReservationList,
    },             
    data() {
      return { 
        
        /* 进入页面时默认进入未完成预约标签页 */
        activeName: 'first',

      }
      
    },created() {

    },
    methods: {
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
    margin:10px 25px 30px 0;

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
    right:25px;
  }


</style>
