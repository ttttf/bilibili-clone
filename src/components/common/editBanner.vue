<template>
  <div>
      <div class="editbanner clearfix">
          <span>{{left}}</span>
          <span @click="BannerClick"><slot name="right"></slot></span>
      </div>
  </div>
</template>

<script>
export default {
    props: ['left'],
    methods: {
        BannerClick() {
            this.$emit('BannerClick')
        }
    }
}
</script>

<style>
.editbanner{
    background-color: #fff;
    border-bottom: 1px solid #eee;
}
.editbanner span{
    padding: 3.889vw 0;
    font-size: 3.889vw;
    display: block;
}
.editbanner span:nth-child(1){
    padding-left: 3.889vw;
    color: #505050;
    text-align: left;
    width: 30%;
    float: left;
}
.editbanner span:nth-child(2){
    padding-right: 4.444vw;
    width: calc(70% - 9.722vw);
    text-align: right;
    float: right;
}
/* 清除浮动 */
.clearfix:after,.clearfix:before{
    content: "";display: table;
}
.clearfix:after{
    clear:both;
}
.clearfix{
    zoom:1;
}
</style>