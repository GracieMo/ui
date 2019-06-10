<template>
  <el-dialog title="新建/编辑来访者" :visible.sync="createOreditVisitorFormVisible">
    <el-form :model="createOreditVisitor" :rules="createOreditVisitor_rules" ref="createOreditVisitor" label-width="100px" class="demo-ruleForm">
      <el-form-item label="姓名" required>
        <el-col :span="11">
          <el-form-item prop="visitor_name">
            <el-input style="width:80px" v-model="createOreditVisitor_rules.visitor_name"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="11">
          <el-form-item prop="visitor_sex">
            <el-select v-model="createOreditVisitor.visitor_sex" placeholder="请选择">
              <el-option label="男" value="男"></el-option>
              <el-option label="女" value="女"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item label="活动区域" prop="region">
        <el-select v-model="createOreditVisitor.region" placeholder="请选择活动区域">
          <el-option label="区域一" value="shanghai"></el-option>
          <el-option label="区域二" value="beijing"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="活动时间" required>
        <el-col :span="11">
          <el-form-item prop="date1">
            <el-date-picker type="date" placeholder="选择日期" v-model="createOreditVisitor.date1" style="width: 100%;"></el-date-picker>
          </el-form-item>
        </el-col>
        <el-col class="line" :span="2">-</el-col>
        <el-col :span="11">
          <el-form-item prop="date2">
            <el-time-picker placeholder="选择时间" v-model="createOreditVisitor.date2" style="width: 100%;"></el-time-picker>
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item label="即时配送" prop="delivery">
        <el-switch v-model="createOreditVisitor.delivery"></el-switch>
      </el-form-item>
      <el-form-item label="活动性质" prop="type">
        <el-checkbox-group v-model="createOreditVisitor.type">
          <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
          <el-checkbox label="地推活动" name="type"></el-checkbox>
          <el-checkbox label="线下主题活动" name="type"></el-checkbox>
          <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
        </el-checkbox-group>
      </el-form-item>
      <el-form-item label="特殊资源" prop="resource">
        <el-radio-group v-model="createOreditVisitor.resource">
          <el-radio label="线上品牌商赞助"></el-radio>
          <el-radio label="线下场地免费"></el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="活动形式" prop="desc">
        <el-input type="textarea" v-model="createOreditVisitor.desc"></el-input>
      </el-form-item>
      <!--<el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>-->
    </el-form>          
    <div slot="footer" class="dialog-footer">
      <el-button @click="resetForm('createOreditVisitor')">取 消</el-button>
      <el-button type="primary" @click="submitForm('createOreditVisitor')">确 定</el-button>
    </div>
  </el-dialog>
</template>
<script>
export default {
  data(){
    return{
      createOreditVisitorFormVisible: false,
      createOreditVisitor: {
        visitor_name: '',
        visitor_sex: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      createOreditVisitor_rules: {
        visitor_name: [
          { required: true, message: '请输入您的姓名', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请选择活动区域', trigger: 'change' }
        ],
        date1: [
          { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
        ],
        date2: [
          { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
        ],
        type: [
          { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
        ],
        resource: [
          { required: true, message: '请选择活动资源', trigger: 'change' }
        ],
        desc: [
          { required: true, message: '请填写活动形式', trigger: 'blur' }
        ]
      },        
      formLabelWidth: '120px',
      UNRinformation: [],       
    }
  },
  methods:{
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!');
          
        } else {
          return false;
                    
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
      this.createOreditVisitorFormVisible = false;
    }       
  }
}
</script>
<style>
.item {
  margin-top: 10px;
  margin-right: 40px;
}
</style>