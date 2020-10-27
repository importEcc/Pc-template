<template>
  <div class="login-container">
    <a-form-model :model="form" :rules="rules" class="login-form" ref="formLogin">
      <div class="title-container">
        <h3 class="title">登录</h3>
      </div>
      <a-form-model-item prop="username">
        <a-input v-model="form.username" type="text" size="large" placeholder="请输入用户名">
          <a-icon slot="prefix" type="user" :style="{ color: 'rgba(0,0,0,.25)' }"/>
        </a-input>
      </a-form-model-item>
      <a-form-model-item prop="password">
        <a-input-password
          v-model="form.password"
          size="large"
          placeholder="请输入密码"
        >
          <a-icon slot="prefix" type="lock" :style="{ color: 'rgba(0,0,0,.25)' }"/>
        </a-input-password>
      </a-form-model-item>
      <a-form-model-item>
        <a-button
          :loading="loading"
          type="primary"
          size="large"
          class="login-button"
          @click="onSubmit">
          Login
        </a-button>
      </a-form-model-item>
    </a-form-model>
  </div>
</template>
<script>
export default {
  name: 'Login',
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请输入用户名'))
      } else if (value.length > 20) {
        callback(new Error('长度不能超过20位'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请填写密码'))
      } else if (value.length < 6) {
        callback(new Error('密码不能少于6位'))
      } else if (value.length > 20) {
        callback(new Error('长度不能超过20位'))
      } else {
        callback()
      }
    }
    return {
      form: {
        username: '',
        password: ''
      },
      loading: false,
      rules: {
        username: [
          { required: true, trigger: ['blur', 'change'], validator: validateUsername }
        ],
        password: [
          { required: true, trigger: ['blur', 'change'], validator: validatePassword }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          this.loading = true
        }
      })
    }
  }
}

</script>

<style lang="less" scoped>
.login-container {
  min-height: 100%;
  width: 100%;
  background-color: #283443;
  overflow: hidden;

  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 160px 35px 0;
    margin: 0 auto;
    overflow: hidden;

    button.login-button {
      padding: 0 15px;
      font-size: 16px;
      height: 40px;
      width: 100%;
    }

    .title-container {
      position: relative;

      .title {
        font-size: 26px;
        color: #eee;
        margin: 0px auto 40px auto;
        text-align: center;
        font-weight: bold;
      }
    }
  }
}
</style>
