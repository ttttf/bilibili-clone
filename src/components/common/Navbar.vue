<template>
  <div class="navbar">
      <div class="logo">
          <img src="@/assets/logo.png" alt="">
      </div>
      <div>
          <p>
              请输入内容
              <van-icon class="inp-icon" name="search" />
          </p>
      </div>
      <div>
          <img :src="imgUrl" alt="" v-if="imgUrl" @click="$router.push('/userinfo')">
          <img src="@/assets/default_img.jpg" alt="" @click="$router.push('/userinfo')" v-else>
          <p>下载App</p>
      </div>
  </div>
</template>

<script>
// 最好每个页面使用父传子方法来更新页面
export default {
    data () {
        return {
            imgUrl: ''
        }
    },
    methods: {
        async UserData() {
        const res = await this.$http.get('/user/' + localStorage.getItem('id'), {
            /* headers: {
            'Authorization': 'Bearer ' + localStorage.getItem('token')
            } */
        })
        this.imgUrl = res.data[0].user_img
        /* console.log(res) */
        }
    },
    created() {
        this.UserData()
    }
}
</script>

<style>
.navbar{
    height: 12.5vw;
    background-color: white;
    display: flex;
}
.logo{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 30.556vw;
}
.logo img{
    width: 60%;
}
.navbar div:nth-child(2){
    flex: 1;
}
.navbar div:nth-child(2) P{
    background-color: #f4f4f4;
    height: 6.667vw;
    border-radius: 3.333vw;
    width: 70%;
    position: relative;
    font-size: 3.333vw;
    line-height: 6.667vw;
    padding-left: 8.333vw;
    color: #999999;
}
.inp-icon{
    position: absolute;
    left: 2.778vw;
    top: 1.667vw;
}
.navbar div:nth-child(3){
    display: flex;
    justify-content: center;
    align-items: center;
}
.navbar div:nth-child(3) img{
    width: 6.667vw;
    height: 6.667vw;
    border-radius: 50%;
}
.navbar div:nth-child(3) p{
    padding: 1.389vw 2.778vw;
    margin: 1.389vw 2.222vw;
    border-radius: 0.833vw;
    background-color: #fb7299;
    color: white;
    font-size: 3.611vw;
}
</style>
