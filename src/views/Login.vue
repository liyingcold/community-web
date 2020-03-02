<template>
 <div class="main" :style="{backgroundImage:'url('+this.images_data.data+')'}" >
  
   <!--  登录框 -->
    <div class="login_bg" style="color" v-show="!isShow">
      <span class="title">LOGIN</span>
      <div class="login_boder">
        <el-form ref="form_login" :rules="login_rule" :model="login_form" class="login_form" >
          <el-form-item class="login_form_item"  prop="username" >
            <el-input class="login_form_input"  type="text" placeholder="用户名" v-model="login_form.username">
            </el-input>
          </el-form-item>
          <el-form-item class="login_form_item" prop="password">
            <el-input class="login_form_input" type="password"  placeholder="密码" v-model="login_form.password">
            </el-input>
          </el-form-item>
          <input type="button" class="login_button" @click="onLogin" value="登录">
        </el-form>
        <button class="toRegister" @click="toeach">立即注册?</button>
      </div>
      <div class="bubble"></div>
    </div>
<!-- 注册 -->
    <div class="register_bg login_bg"  v-show="isShow">
      <div class="icon_back">
        <i class="el-icon-back" @click="toeach" ></i>
      </div>
       <br>
       <span class="title">Register</span>
       <div class="login_boder">
         <el-form ref="form_register" :rules="register_rule" :model="register_form">
           <el-form-item class="login_form_item" prop="name">
            <el-input class="login_form_input" type="text" placeholder="请输入用户名" v-model="register_form.name">
            </el-input>
          </el-form-item>
          <el-form-item class="login_form_item" prop="password">
            <el-input class="login_form_input"  type="password" placeholder="请输入密码" v-model="register_form.password">
            </el-input>
          </el-form-item>
          <!-- <el-form-item class="login_form_item" prop="form_email">
            <el-input class="login_form_input"   placeholder="请输入邮箱" v-model="register_form.form_email">
            </el-input>
          </el-form-item> -->
          <input class="register_botton login_button" type="button" @click="onRegister" value="注册">
        </el-form>
       
       </div>
        
      <div class="bubble"></div>
    </div>
 </div>
    
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      msg: "1212",
      images_data: [],
      isShow:false,
      login_form:{
        username:'',
        pswd:'',
      },
      register_form:{
        name:'',
        password:'',
        // form_email:''
      },
      login_rule:{
        username:[{required: true, message: '请输入用户名', trigger: 'change'}],
        password:[{required: true, message: '请输入密码', trigger: 'change' }],
      },
      register_rule:{
        name:[{required: true, message: '请输入用户名', trigger: 'change'}],
        password:[{required: true, message: '请输入密码', trigger: 'change' }],
        // form_email:[{required: true, message: '请输入邮箱', trigger: 'change'}]
      }    
    }
  },
  
   
  methods: {
    // 获取图片主色调
    GetImgColor(){
      
    },
    // 登录<==>注册
    toeach(){
      this.isShow = !this.isShow;
    },
    // 登录
    onLogin(){
      console.log(this.login_form)
      this.$refs.form_login.validate(t=>{
        console.log(t)
        if(t){
          this.$axios({
            url:'http://localhost:8800/api/user/login',
            method:'post',
            params:this.login_form
          }).then((res)=>{
            console.log(res)
            if(res.data.status == 0){
                this.$message({
                  message:res.data.msg,
                  type:'success'
              }),
              this.$refs['form_login'].resetFields();
            }
             if(res.data.status == 1){
               this.$message({
                message:res.data.msg,
                type:'warning'
                })
            }
          })
        }
      })
    },
    // 注册
    onRegister(){
      console.log(this.register_form)
      this.$refs.form_register.validate(t=>{
        if(t){
          this.$axios({
            url:'http://localhost:8800/api/user/register',
            method:'post',
            params:this.register_form
          }).then((res)=>{
            console.log(res)
            if(res.data.status == 0){
               this.$message({
                message:res.data.msg,
                type:'success'
                 }),
                this.$refs['form_register'].resetFields();
                this.isShow = !this.isShow
               
            }
            if(res.data.status == 1){
               this.$message({
                message:res.data.msg,
                type:'warning'
            }),
             this.$refs['form_register'].resetFields();
            }
            })
        }
      })
    }
  },
  mounted() {
    this.$axios({
      // url:'https://free-api.heweather.net/s6/weather/now?location=beijing&key=46a723541ce941e9ae69efaad9a9e8a5',
      url:'http://localhost:8800/api/bing/pic',
      method:'get'
    }).then(res=>{
      this.images_data=res.data;
      console.log(this.images_data.data)
    })
    
  }
}
</script>
<style> 
.main{
  width: calc(100vw);
  height: calc(100vh);
}
.login_bg {
  position: absolute;
  width: calc(100vw / 5.48);
  height: calc(100vh /2.34);
  margin-left: calc((100vw - 350px) / 2);
  margin-top: calc((100vh - 400px) / 3);
  min-width: 350px;
  min-height: 400px;
  padding-top:30px;
  text-align: center;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#3f000000',endColorstr='#3f000000');
  background-color: rgba(255, 255, 255, 0.15);
  border-radius: 5px;
  box-shadow: 0 0 10px 6px rgb(0,0,0, 0.5);
}
/* title */
.title {
  color: rgb(255, 255, 255);
  font-size: 20px;
}
.icon_back i{
  float: left;
  margin-left: 6%;
  
}
.login_boder{
  width: 75%;
  height: 70%;
  margin-left: 12.5%;
}
.el-form{
  width: 100%;
  height: 100%;
}

/* 输入框 */
input.el-input__inner{
  margin-top: 10%;
  -webkit-appearance: none;
  background-color:  rgba(255, 255, 255, 0);
  background-image: none;
  border: none;
  border-bottom: 2px solid  rgba(255, 255, 255, 0.5);
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  color:  rgb(255, 255, 255);
  display: inline-block;
  font-size: inherit;
  width: 100%;
  outline: 0;
  padding: 0 15px;
  -webkit-transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
  transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
}
.el-input.is-active .el-input__inner, .el-input__inner:focus{
  border-color: rgba(255, 255, 255, 0.5) !important;
}


/* placeholder */
.login_::-webkit-input-placeholder {
    color: rgba(255, 255, 255, 0.39);
    font-size: 15px;
}
.login_:-moz-placeholder {
    color:  rgba(255, 255, 255, 0.39);
    font-size: 15px;
}
.login_:-ms-input-placeholder {
    color:  rgba(255, 255, 255, 0.39);
    font-size: 15px;
}
/* 登录按钮 */
.login_button{
    width: 80px;
    height: 15%;
    line-height: 1;
    white-space: nowrap;
    cursor: pointer;
    background: rgba(255, 255, 255, 0.3);
    border: none;
    -webkit-appearance: none;
    text-align: center;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    outline: 0;
    /* margin-top: 60px; */
    margin-top: 10%;
    -webkit-transition: .1s;
    transition: .1s;
    font-size: 15px;
    font-weight: 900;
    color: #fff;
    border-radius: 5px;
}
   
/* 小尾巴 */
.bubble {
  content: "";
  position: absolute;
  top: 100%;
  right: 7px;
  width: 100px;
  height: 16px;
  border-width: 0;
  border-style: solid;
  border-color: transparent;
  margin-top: 0px;
  border-left-width: 8px;
  border-left-color: currentColor;
  border-radius: 0 0 0 200px;
  color: rgba(255, 255, 255, 0.15);
}
/*注册按钮*/
.toRegister{
  
  float:right;
  cursor: pointer;
  background: rgba(255, 255, 255, 0);
  border: none;
  -webkit-appearance: none;
  text-align: center;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-transition: .1s;
  transition: .1s;
  font-size: 15px;
  color: #fff;
  border-radius: 5px;
}
.el-icon-back{
  
  cursor: pointer;
  color: rgb(253, 253, 253);
}
 
</style>