<template>
  <div class="login-container">
    <div class="loginFrom">
      <a-card class="login" :bordered="false" :body-style="{ width: '480px', padding: '30px 0' }">
        <div class="login_right_container">
          <div class="title_box">
            <h2 class="title">{{ APP_TITLE }}</h2>
          </div>
          <!-- form -->
          <login-form />
        </div>
      </a-card>
    </div>
    <div class="loginImage">
      <img src="../../assets/images/christmas-3.png" class="lgImage" />
    </div>
  </div>
</template>
<script setup lang="ts">
  import LoginForm from './Form.vue';
  import { APP_TITLE } from '../../../config/constant';
</script>
<style lang="less" scoped>
  .login-container {
    width: 100vw;
    height: 100vh;
    background: #fff;
    padding: 0 40px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;

    .login {
      border-radius: 10px;
      // box-shadow: 0 3px 10px rgba(0, 0, 0, 0.4);
      &_right {
        padding-top: 80px;

        &_container {
          width: 360px;
          margin: 0 auto;
        }
      }
    }
  }

  .loginImage {
    margin-left: 100px;

    .lgImage {
      width: 450px;
    }
  }

  .title_box {
    display: flex;

    .title {
      font-size: 22px;
      color: #000000;
    }
  }
</style>
