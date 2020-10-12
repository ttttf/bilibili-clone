<template>
  <div class="userinfo">
    <nav-bar></nav-bar>
    <div class="banner">
      <img src="@/assets/bannerTop_new.png" alt="" class="backImg">
    </div>
    <user-detail :userInfo="model" />
    <user-article />
  </div>
</template>

<script>
import NavBar from '../components/common/Navbar'
import userDetail from '../components/usercomponents/userDetail'
import userArticle from '../components/usercomponents/userArticle'

export default {
  data() {
    return {
      model: {}
    }
  },
  components: {
    NavBar,
    userDetail,
    userArticle
  },
  methods: {
    async UserinfoData() {
      const res = await this.$http.get('/user/' + localStorage.getItem('id'), {
        /* headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        } */
      })
      this.model = res.data[0]
      /* console.log(res) */
    }
  },
  created() {
    this.UserinfoData()
  }
}
</script>

<style>
.banner{
  height: 25vw;
  overflow: hidden;
  width: 100%;
}
.backImg{
  height: 36.111vw;
  width: 100%;
}
</style>
