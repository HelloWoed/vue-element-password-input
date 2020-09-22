<template>
  <div class="hello">
    <h1>密码输入框</h1>
    <div class="loginForm">
      <el-form size="medium" :model="loginForm" ref="loginForm" :rules="loginRules">
          <el-form-item prop="username">
              <el-input
                  placeholder="请输入用户名"
                  prefix-icon="el-icon-user"
                  v-model="loginForm.username"
                  ></el-input>
          </el-form-item>
          <el-form-item prop="password">
            <vue-element-password-input 
            v-model="loginForm.password" 
            prefixIcon="el-icon-lock"
            placeholder="请输入密码" 
            inputSize="medium"
            :maxlength="16" />
          </el-form-item>
          <el-form-item>
              <el-button type="primary" class="handleLogin" @click.native.prevent="handleLogin">登录</el-button>
          </el-form-item>
          <el-row type="flex" justify="end">
              <el-link :underline="false" type="primary" @click="jumpForgetPasswd">忘记密码</el-link>
          </el-row>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      loginForm:{},
    }
  },
  computed:{
    loginRules(){
      return {
        password: [
          {required: true,message: '请输入密码', trigger: 'blur'},
          {validator: this.validPassword, trigger: "blur"}
        ]
      }
    }
  },
  methods:{
    validPassword(rule, value, callback){
      let reg = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[^]{8,16}$/;
      if(reg.test(value)){
        callback();
      }else{
        callback(new Error('密码包含大小写字母和数字！'));
      }
    },
    jumpForgetPasswd(){

    },
    handleLogin(){
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.loginForm{
  padding: 0 30%;
}
</style>
