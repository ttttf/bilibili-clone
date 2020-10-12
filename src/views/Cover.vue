<template>
  <div>
      <div class="video-con" @click="$router.push(`/article/${coveritem.id}`)">
          <div class="card">
                <img :src="coveritem.img" alt="" style="width: 100%; height: 100%;">
                <div class="count">
                    <span class="count-play">
                        <div class="svg-play"><img src="../assets/play.svg" alt="" style="height: 3.333vw; width: 3.333vw;"></div>
                        <span><!-- {{coveritem.playlen}} -->123</span>
                    </span>
                    <span class="count-comment">
                        <div class="svg-comment"><img src="../assets/comment.svg" alt="" style="height: 3.333vw; width: 3.333vw;"></div>
                        <span v-if="coveritem.commentlen">{{coveritem.commentlen}}</span>
                        <span v-else>60</span>
                    </span>
                </div>
          </div>
          <p class="name">{{coveritem.name}}</p>
      </div>
  </div>
</template>

<script>

export default {
    props: ['coveritem']
}
</script>

<style scoped>
.video-con{
    padding: 2.222vw 1.111vw;
}
.video-con p{
    color: #212121;
    margin: 0;
    margin-top: 1.667vw;
    height: 8.333vw;
    font-size: 2.778vw;
    overflow: hidden;
    -webkit-line-clamp: 2;
    text-overflow: ellipsis;
}
.card{
    position: relative;
    width: 100%;
    height: 27.778vw;
}
.count{
    position: absolute;
    bottom: 0;
    left: 0;
    width: calc(100% - 3.333vw);
    font-size: 3.611vw;
    padding: 1.389vw 1.667vw;
    color: #fff;
    background: linear-gradient(0deg,rgba(0,0,0,.85),transparent);
}
.count-play{
    display: block;
    float: left;
}
.count-comment{
    display: block;
    float: right;
}
.name{
    height: 10vw;
    font-size: 2.778vw;
    overflow: hidden;
    text-overflow: ellipsis;
}
.svg-play{
    display: inline-block;
}
.svg-comment{
    display: inline-block;
}
</style>