<template>
  <div class="login-container">
    <div class="el-form login-form el-form--label-left">
      <div class="title-container">
        <!-- <img src="../assets/images/cadtech.png" alt=""> -->
        <h3 class="title">凱德鈑金系統</h3>
      </div>
      <div class="el-form-item">
        <el-input
          ref="account"
          v-model="account"
          placeholder="帳號"
          name="account"
          type="text"
          tabindex="1"
          auto-complete="on"
        />
      </div>
      <div class="el-form-item">
        <el-input
          key="password"
          ref="password"
          v-model="password"
          type="password"
          placeholder="密碼"
          name="password"
          tabindex="2"
          auto-complete="on"
          @keyup.enter.native="login"
        />
      </div>
      <el-button type="primary" style="width:100%;margin-bottom:30px;background-color: teal; border-color: teal" @click="login">Login</el-button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data: () => ({
    account: '',
    password: '',
    rememberMe: false,
    error: false,
  }),
  methods: {
    async login () {
      this.$router.push({ name: 'Dashboard' })
      try {
        await axios.post('/Auth/Login', {
          Account: this.account,
          Password: this.password,
          RememberMe: this.rememberMe
        })
        await this.$router.push({ name: 'Dashboard' })
      } catch (e) {
        this.error = true
      }
    }
  }
}
</script>

<style lang="scss">
$bg: #283443;
$light_gray: #fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
  }
}

/* reset element-ui css */
.login-container {
  height: 100%;

  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;

    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
  }

  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
}
</style>

<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;

  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 160px 35px 0;
    margin: 0 auto;
    overflow: hidden;
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
    }
  }

  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }
}
</style>
