<script>
import userUtils from "@/utils/userUtils";

export default {
  name: "LoginDialog",
  mixins:[userUtils],
  data(){
    return{
      registerVisible: false,
      account:'',
      password:''
    }
  },
  computed: {
    formTransform() {
      return this.registerVisible ? 'translateX(80%)' : 'translateX(0%)';
    }
  },
  methods:{
    showRegister() {
      this.registerVisible = true;
    },

    showLogin() {
      this.registerVisible = false;
    },

    async userRegisterFromDialog(){
      try{
        await this.userRegister(this.account, this.password);
        window.alert('注册成功，请点击登录按钮进行登录');
      }catch (e){
        window.alert('注册失败');
      }
    },

    async userLoginFromDialog(){
      try {
        await this.userLogin(this.account, this.password);
        location.reload();
      }catch (e){
        window.alert('登录失败');
      }
    }
  }
}
</script>

<template>

  <div class="user-login-form-container">
    <div class="container">
      <div class="form-box" :style="{ transform: formTransform }">
        <div class="register-box" :class="{ hidden: !registerVisible }">
          <h1>register</h1>
          <input type="text" placeholder="请输入账号" v-model="account">
          <input type="password" placeholder="请输入密码" v-model="password">
          <button @click="userRegisterFromDialog">注册</button>
        </div>
        <div class="login-box" :class="{ hidden: registerVisible }">
          <h1>login</h1>
          <input type="text" placeholder="请输入账号" v-model="account">
          <input type="password" placeholder="请输入密码" v-model="password">
          <button @click="userLoginFromDialog">登录</button>
        </div>
      </div>
      <div class="con-box left">
        <h2>欢迎来到<span>EV网站</span></h2>
        <p>快来看看新发布的<span>视频</span>吧</p>
        <img :src="require('@/assets/ev.png')" alt="">
        <p>已有账号</p>
        <button @click="showLogin">去登录</button>
      </div>
      <div class="con-box right">
        <h2>欢迎来到<span>EV网站</span></h2>
        <p>快来看看新发布的<span>视频</span>吧</p>
        <img :src="require('@/assets/ev.png')" alt="">
        <p>没有账号？</p>
        <button @click="showRegister">去注册</button>
      </div>
    </div>
  </div>

</template>

<style scoped lang="less">
.user-login-form-container {
  /* 弹性布局 水平+垂直居中 */
  display: flex;
  justify-content: center;
  align-items: center;
  /* 渐变背景 */
  background: linear-gradient(200deg, #f3e7e9, #e3eeff);
}
.container {
  background-color: #fff;
  width: 650px;
  height: 415px;
  border-radius: 5px;
  /* 相对定位 */
  position: relative;
}
.form-box {
  /* 绝对定位 */
  position: absolute;
  top: -10%;
  left: 5%;
  background-color: #d3b7d8;
  width: 320px;
  height: 520px;
  border-radius: 5px;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2;
  /* 动画过渡 加速后减速 */
  transition: 0.5s ease-in-out;
}
.register-box,
.login-box {
  /* 弹性布局 垂直排列 */
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
.hidden {
  display: none;
  transition: 0.5s;
}
h1 {
  text-align: center;
  margin-bottom: 25px;
  /* 大写 */
  text-transform: uppercase;
  color: #fff;
  /* 字间距 */
  letter-spacing: 5px;
}
input {
  background-color: transparent;
  width: 70%;
  color: #fff;
  border: none;
  /* 下边框样式 */
  border-bottom: 1px solid rgba(255, 255, 255, 0.4);
  padding: 10px 0;
  text-indent: 10px;
  margin: 8px 0;
  font-size: 14px;
  letter-spacing: 2px;
}
input::placeholder {
  color: #fff;
}
input:focus {
  color: #a262ad;
  outline: none;
  border-bottom: 1px solid #a262ad80;
  transition: 0.5s;
}
input:focus::placeholder {
  opacity: 0;
}
.form-box button {
  width: 70%;
  margin-top: 35px;
  background-color: #f6f6f6;
  outline: none;
  border-radius: 8px;
  padding: 13px;
  color: #a262ad;
  letter-spacing: 2px;
  border: none;
  cursor: pointer;
}
.form-box button:hover {
  background-color: #a262ad;
  color: #f6f6f6;
  transition: background-color 0.5s ease;
}
.con-box {
  width: 50%;
  /* 弹性布局 垂直排列 居中 */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* 绝对定位 居中 */
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
.con-box.left {
  left: -2%;
}
.con-box.right {
  right: -2%;
}
.con-box h2 {
  color: #8e9aaf;
  font-size: 25px;
  font-weight: bold;
  letter-spacing: 3px;
  text-align: center;
  margin-bottom: 4px;
}
.con-box p {
  font-size: 12px;
  letter-spacing: 2px;
  color: #8e9aaf;
  text-align: center;
}
.con-box span {
  color: #d3b7d8;
}
.con-box img {
  width: 150px;
  height: 150px;
  opacity: 0.9;
  margin: 40px 0;
}
.con-box button {
  margin-top: 3%;
  background-color: #fff;
  color: #a262ad;
  border: 1px solid #d3b7d8;
  padding: 6px 10px;
  border-radius: 5px;
  letter-spacing: 1px;
  outline: none;
  cursor: pointer;
}
.con-box button:hover {
  background-color: #d3b7d8;
  color: #fff;
}

// 手机端样式，适用于宽度小于或等于1080px的屏幕
@media (max-width: 1080px) {
  .user-login-form-container {
    /* 弹性布局 水平+垂直居中 */
    display: flex;
    justify-content: center;
    align-items: center;
    /* 渐变背景 */
    background: linear-gradient(200deg, #f3e7e9, #e3eeff);
  }
  .container {
    background-color: #fff;
    width: 650px;
    height: 415px;
    border-radius: 5px;
    /* 相对定位 */
    position: relative;
  }
  .form-box {
    /* 绝对定位 */
    position: absolute;
    top: -10%;
    left: 5%;
    background-color: #d3b7d8;
    width: 320px;
    height: 520px;
    border-radius: 5px;
    box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 2;
    /* 动画过渡 加速后减速 */
    transition: 0.5s ease-in-out;
  }
  .register-box,
  .login-box {
    /* 弹性布局 垂直排列 */
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  }
  .hidden {
    display: none;
    transition: 0.5s;
  }
  h1 {
    text-align: center;
    margin-bottom: 25px;
    /* 大写 */
    text-transform: uppercase;
    color: #fff;
    /* 字间距 */
    letter-spacing: 5px;
  }
  input {
    background-color: transparent;
    width: 70%;
    color: #fff;
    border: none;
    /* 下边框样式 */
    border-bottom: 1px solid rgba(255, 255, 255, 0.4);
    padding: 10px 0;
    text-indent: 10px;
    margin: 8px 0;
    font-size: 14px;
    letter-spacing: 2px;
  }
  input::placeholder {
    color: #fff;
  }
  input:focus {
    color: #a262ad;
    outline: none;
    border-bottom: 1px solid #a262ad80;
    transition: 0.5s;
  }
  input:focus::placeholder {
    opacity: 0;
  }
  .form-box button {
    width: 70%;
    margin-top: 35px;
    background-color: #f6f6f6;
    outline: none;
    border-radius: 8px;
    padding: 13px;
    color: #a262ad;
    letter-spacing: 2px;
    border: none;
    cursor: pointer;
  }
  .form-box button:hover {
    background-color: #a262ad;
    color: #f6f6f6;
    transition: background-color 0.5s ease;
  }
  .con-box {
    width: 50%;
    /* 弹性布局 垂直排列 居中 */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* 绝对定位 居中 */
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }
  .con-box.left {
    left: -2%;
  }
  .con-box.right {
    right: -2%;
  }
  .con-box h2 {
    color: #8e9aaf;
    font-size: 25px;
    font-weight: bold;
    letter-spacing: 3px;
    text-align: center;
    margin-bottom: 4px;
  }
  .con-box p {
    font-size: 12px;
    letter-spacing: 2px;
    color: #8e9aaf;
    text-align: center;
  }
  .con-box span {
    color: #d3b7d8;
  }
  .con-box img {
    width: 150px;
    height: 150px;
    opacity: 0.9;
    margin: 40px 0;
  }
  .con-box button {
    margin-top: 3%;
    background-color: #fff;
    color: #a262ad;
    border: 1px solid #d3b7d8;
    padding: 6px 10px;
    border-radius: 5px;
    letter-spacing: 1px;
    outline: none;
    cursor: pointer;
  }
  .con-box button:hover {
    background-color: #d3b7d8;
    color: #fff;
  }
}
</style>