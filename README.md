# vue-element-password-input

## 安装
```
npm install vue-element-password-input
```

### 引入
```javascript
// main.js
import passwordInput from 'vue-element-password-input'

Vue.use(passwordInput);
```

### 使用
<!-- 支持v-model绑定 -->
```html
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
```
```javascript
...
data(){
    return {
      loginForm:{},
    }
},
computed:{
    loginRules(){
      return {
        password: [
          {required: true,message: '请输入密码', trigger: 'change'}
        ]
      }
    }
},
...
```
