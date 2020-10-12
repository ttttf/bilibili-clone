<template>
  <div>
    <login-top middleTop="登录bilibili">
      <div slot="right" style="font-size:3.611vw" @click="$router.push('/register')">切换到注册</div>
    </login-top>
    <login-text label="账号"
      style="margin:4.167vw 0"
      placeholder="请输入账号"
      rule="^.{6,16}"
      @inputChange="res => model.username = res"
    />
    <login-text label="密码"
      rule="^.{6,16}"
      placeholder="请输入密码"
      @inputChange="res => model.password = res"
    />
    <login-btn btntext="登录" @registerSubmit="registerSubmit"></login-btn>
  </div>
</template>

<script>
import LoginTop from '../components/common/LoginTop'
import LoginText from '../components/common/LoginText'
import LoginBtn from '../components/common/LoginBtn'

export default {
  data () {
    return {
      model: {
        username: '',
        password: ''
      }
    }
  },
  components: {
    LoginTop,
    LoginText,
    LoginBtn
  },
  methods: {
    // 用async await 让异步数据变为同步数据
    async registerSubmit () {
      let rulg = /^.{6,16}$/
      if (rulg.test(this.model.username) && rulg.test(this.model.password)) {
        const res = await this.$http.post('/login', this.model)
        this.$msg.fail(res.data.msg)
        console.log(res)
        if (res.data.code == 200) {
          localStorage.setItem('id',res.data.id)
          localStorage.setItem('token',res.data.token)
          setTimeout(() => {
            this.$router.push('/userinfo')
          },1000)
        }
        /* ------------------------------------------------------------ */
      } else {
        this.$msg.fail('格式不正确，请重新输入')
      }
    }
  }
}
</script>

<style>

</style>
