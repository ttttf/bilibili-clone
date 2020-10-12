<template>
  <div class="article" v-if="model">
      <nav-bar></nav-bar>
      <!-- 视窗 -->
      <div class="windows">

          <div class="video">
            <!-- 本处应为 :src="model.content" -->
            <!-- <video id="0" controls="controls" src="https://cn-hnzz-cmcc-v-06.bilivideo.com/upgcxcode/87/69/201056987/201056987-1-16.mp4?expires=1592323200&platform=html5&ssig=2gn02oXWaGEiDE1uq8Mf4g&oi=1972811377&trid=22f1f80030804d2291e362c2c5730081h&nfc=1&nfb=maPYqpoel5MI3qOUX6YpRA==&mid=372412242&logo=80000000"></video>
             --><video id="0" controls="controls" :src="model.content"></video>
            <div class="load-layer" :class="{hide: active}" @click="Hide">
                <img :src="model.img" alt="" style="width: 100%; height: 100%;position:relative;">
                <i class="play-bottom">
                    <div><img src="../assets/play.svg" alt="" style="height: 13.889vw; width: 13.889vw;"></div>
                </i>
            </div>
          </div>

          <div class="detail-info">
              <a href="javascript:;" class="label">
                <span>活动</span>
              </a>
              <h1>{{model.name}}</h1>
              <div class="user-data">
                  <a href="javascript:;" class="up-info">
                    <span class="up">up</span>
                    <span class="user-name">{{model.userinfo.name}}</span>
                  </a>
                  <span class="scan">146.4万次观看</span>
                  <span class="danmuku">5281弹幕</span>
                  <span class="date">{{model.date}}</span>
              </div>
          </div>

      </div>
        <!-- 三连 -->
      <div class="triple">
            <span class="click-item">
                <img src="../assets/like.svg" alt="" style="height: 5.556vw;width:5.556vw;">
                <span>点赞</span>
            </span>
            <span class="click-item">
                <img src="../assets/collect.svg" alt="" style="height: 5.556vw;width:5.556vw;">
                <span>收藏</span>
            </span>
            <span class="click-item">
                <img src="../assets/download.svg" alt="" style="height: 5.556vw;width:5.556vw;">
                <span>缓存</span>
            </span>
      </div>
      <!-- 推荐文章或视频 -->
      <div>
        <!-- 
            监测路由变化以重新渲染文章，
            或者在app.vue目录下，对<router-view></router-view>进行摧毁和重建(通过变量routerAlive的状态控制)，页面会进行重新渲染。
         -->
          <cover class="cover-video" v-for="(item, index) in commendList" :key="index" :coveritem="item" />
      </div>

  </div>
</template>

<script>
import NavBar from '../components/common/Navbar'
import Cover from '../views/Cover'

export default {
    data() {
        return {
            model: null,
            commendList: null,
            active: false
        }
    },
    components: {
        NavBar,
        Cover
    },
    methods: {
        // 根据文章id添加数据
        async articleItemData() {
            /* console.log(this.$route) */
            const res = await this.$http.get('/article/' + this.$route.params.id)
            /* console.log(res) */
            this.model = res.data[0]
        },
        Hide() {
            this.active = true
            // 获取video元素，点击触发播放事件
            document.getElementById('0').play()
        },
        // 获取推荐文章或视频
        async commendData() {
            const res = await this.$http.get('/commend')
            /* console.log(res) */
            this.commendList = res.data
        }
    },
    created() {
        this.articleItemData()
        this.commendData()
    },
    watch: {
        // 路由改变，重新渲染文章，初始化
        $route() {
            this.active = false
            this.commendList = false
            this.model = null
            this.articleItemData()
            this.commendData()
        }
    }
}
</script>

<style scoped>
.article{
    background-color: #fff;
}
.video{
    position: relative;
    height: 55.556vw;
}
.load-layer{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 55.556vw;
}
.play-bottom{
    position: absolute;
    top: 20.833vw;
    left: calc((100% - 13.889vw)/2);
}
.video video{
    width: 100%;
    height: 100%;
}
.detail-info{
    position: relative;
    padding: 0 2.778vw;
    margin-top: 4.444vw;
}
.detail-info h1{
    font-size: 4.444vw;
    font-weight: 400;
    display: inline-block;
    color: #212121;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 83.333vw;
    line-height: 6.667vw;
    padding-left: 13.889vw;
    margin: 0;
}
.label{
    position: absolute;
    background-color: #f4f4f4;
    font-size: 3.333vw;
    color: #fb7299;
    height: 6.667vw;
    border-radius: 3.333vw;
    width: 8.333vw;
    text-align: center;
    line-height: 6.667vw;
    top: 0;
}
.hide{
    display: none;
}
.user-data{
    font-size: 3.333vw;
    margin-top: 2.222vw;
}
.up{
    display: block;
    float: left;
    border: 0.278vw solid rgb(122, 114, 114);
    border-radius: 0.833vw;
    font-size: 2.778vw;
    color: #000;
}
.user-name{
    float: left;
    display: block;
    width: 27.778vw;
    height: 4.444vw;
    overflow: hidden;
    text-overflow: ellipsis;
    font-size: 3.333vw;
    color: #212121;
    margin-right: 5.556vw;
    margin-left: 1.389vw;
}
.scan{
    color: #999;
    font-size: 3.333vw;
    margin-right: 2.778vw;
}
.danmuku{
    font-size: 3.333vw;
    margin-right: 2.778vw;
    color: #999;
}
.date{
    font-size: 3.333vw;
    display: inline-block;
    color: #999;
}
.triple{
    padding: 3.611vw 3.889vw;
    color: #999;
}
.click-item span{
    font-size: 3.333vw;
    vertical-align: middle;
    display: inline-block;
    vertical-align: middle; 
}
.click-item img{
    vertical-align: middle; 
    margin-right: 1.389vw;
}
.click-item{
    display: inline-block;
    margin-right: 5.556vw;
    font-size: 0;
    
    height: 5.556vw;
}
.cover-video{
  width: 50%;
  display: inline-block;
}
</style>
