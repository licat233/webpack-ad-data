<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/images/avatar.jpg" />
      </div>
      <el-form :model="loginForm" :rules="loginFormRules" ref="loginFormRef" label-width="0px" class="login_form">
        <!--用户名-->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="el-icon-user" placeholder="请输入账号"></el-input>
        </el-form-item>
        <!--密码-->
        <el-form-item prop="password">
          <el-input
            v-model="loginForm.password"
            prefix-icon="el-icon-lock"
            placeholder="请输入密码"
            show-password
          ></el-input>
        </el-form-item>
        <!--按钮-->
        <el-form-item class="btns">
          <el-button type="primary" @click="submitLoginForm()">登录</el-button>
          <el-button type="info" @click="resetLoginForm()">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 这是登陆表单的数据绑定对象
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      // 这是表单的验证规则
      loginFormRules: {
        // 验证用户名是否合法
        username: [
          { required: true, message: '请输入账号', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        // 验证密码是否合法
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 10, message: '长度在 6 到 12 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    submitLoginForm () {
      this.$refs.loginFormRef.validate(
        async valid => {
          if (!valid) return false
          const { data: res } = await this.$http.post('login', this.loginForm)
          if (res.meta.status !== 200) return this.$message.error('登录失败！')
          this.$message.success('登录成功！')
          // 1.将登陆成功之后的 token ，保存到客户端的 sessionStorage 中
          // 1.1项目中除了登录之外的其它API接口，必须在登录之后才能访问
          // 1.2 token 只应在当前网站打开期间生效，所以将 token 保存到 sessionStorage中
          window.sessionStorage.setItem('token', res.meta.token)
          // 2.通过编程式导航跳转到后台主页，路由地址是 /home
          this.$router.push('/home')
        }
      )
    },
    resetLoginForm () {
      this.$refs.loginFormRef.resetFields()
    }
  }
}
</script>

<style lang="less" scoped>
.login_container {
  background-image: linear-gradient(to Top, #0099ff, #ffffff);
  height: 100%;
}
.login_box {
  width: 350px;
  height: 280px;
  background-color: #ffffff;
  box-shadow: 0px 0px 10px #bbb;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avatar_box {
  width: 100px;
  height: 100px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 8px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}
.btns {
  display: flex;
  justify-content: flex-end;
}
.login_form {
  position: absolute;
  bottom: 0px;
  width: 100%;
  padding: 0px 20px;
  box-sizing: border-box;
}
</style>
