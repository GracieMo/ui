<template>
    <div>
        <div>
            <el-row class='Loginback'>
                <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="2"></el-col>
                <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="10">
                    <img  class="Loginimg" src="..\assets\img\login.png">
                </el-col>
                <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="10">
                    <div class="Loginpanel">
                    </div>
                    <div>
                        <img  class="Loginicon" src="..\assets\img\loginlogo.png">
                    </div>
                    <div>
                        <input 
                            type="text" 
                            class="logininput"
                            :placeholder="username"
                        >        
                    </div>
                    <div>
                        <input 
                            type="text" 
                            class="logininput"
                            :placeholder="password"
                            style="margin-top:3.5%"
                        >        
                    </div>
                    <div>
                        <el-button class='loginbutton'>登录</el-button>      
                    </div>
                    <div>
                        <el-checkbox>记住密码</el-checkbox>         
                    </div>                
                </el-col>
                <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="2"></el-col>
            </el-row>
        </div>
        <!-- <div class="Logintext">
            本网站版权归xxxxxxx团队所有，未经许可，不得转载
        </div> -->
    </div>
</template>




<script>
    export default{
        data(){
            return{
                username:'\ue8e9  请输入用户名',
                password:'\ue628  请输入密码'
            }
        },
        method:{
            valid(){
                
            }
        }
    }
</script>

<style>
.Loginback{
    width:100%;
    height:60%;
    position:absolute;
    top:20%;
    background-color:#ECF5FF;
}
/* .Logintext{
    top:80%;
    width:100%;
    text-align:center;
    position:absolute;
} */
.Loginimg{

    width:30%;
    height:100%;
    left:15%;
    top:0;
    position: absolute;
}
.Loginpanel{
    background-color: #fff;
    border-radius: 8px;
    width:20%;
    height:80%;
    left:63%;
    top:10%;
    position: absolute;
    opacity: 0.6;
    border:none;

}
.Loginicon{
    position: absolute;
    width:2.5%;
    height:8%;
    left:71.5%;
    top:15%;

}
.logininput{
    position: absolute;
    width:15.5%;
    height:8%;
    top:30%;
    left:65%;
    border-radius: 8px;
    border:1px solid #F0F0F0;
    padding-left:0.5%;
    font-family: 'iconfont';
    font-size:14px;
    color:#515151;
}
.loginbutton{
    position: absolute;
    width:16%;
    height:8%;
    top:45%;
    left:65%;
    border-radius: 8px;
    border:none;
    font-size:16px;
    color:#fff;
    margin-top:3.4%;
    text-align: center;
    background-color: #84B2BF;
    cursor:pointer;
}
 .loginbutton:hover,.loginbutton:focus{
    position: absolute;
    width:16%;
    height:8%;
    top:45%;
    left:65%;
    border-radius: 8px;
    border:none;
    font-size:16px;
    color:#fff;
    margin-top:3.4%;
    text-align: center;
    background-color: #84B2BF;
    cursor:pointer;
  }
  .loginbutton:active{
    position: absolute;
    width:16%;
    height:8%;
    top:45%;
    left:65%;
    border-radius: 8px;
    border:1px solid #84B2BF;
    font-size:16px;
    color:#84B2BF;
    margin-top:3.4%;
    text-align: center;
    background-color: #fff;
    cursor:pointer;
  }
.el-checkbox{
    position: absolute;
    top:72%;
    left:65%;
}
.el-checkbox__label{
    padding-left:5px;
    color:#515151;
}
.el-checkbox__inner:hover{
    border:1px solid#84B2BF;
}
.el-checkbox__input.is-checked .el-checkbox__inner{
    border:1px solid#84B2BF;
    background-color:#84B2BF;

}
.el-checkbox__input.is-focus .el-checkbox__inner{
    border:1px solid#84B2BF;

}
.el-checkbox__input.is-checked+.el-checkbox__label{
    color:#515151;
    font-weight: bolder;
}

</style>


