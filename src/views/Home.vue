<template>
  <div class="home" v-if="category">
    <nav-bar></nav-bar>
    <van-tabs v-model="active" swipeable>
      <van-tab v-for="(item,index) in category" :key="index" :title="item.title">
        <!-- 当组件滚动到底部时，会触发load事件 -->
        <van-list
          v-model="item.loading"
          :finished="item.finished"
          finished-text="我也是有底线的"
          @load="onLoad"
          :immediate-check="false"
        >
          <cover class="cover-video" :coveritem="categoryitem" v-for="(categoryitem, categoryindex) in item.list" :key="categoryindex" />
        </van-list>
      </van-tab>
    </van-tabs>
  </div>
</template>

<script>
import NavBar from '../components/common/Navbar'
import Cover from './Cover'

export default {
    data() {
      return {
        category: [],
        active: 0
      }
    },
    /* name:'Home', */
    components:{
        NavBar,
        Cover
    },
    methods: {
      // 获取导航栏数据
      async selectCategory(){
        const res = await this.$http.get('/category')
        /* console.log(res)
        this.category = res.data */
        this.changeCategory(res.data)
      },
      // 重新封装category,初始化页面
      changeCategory(data) {
        const category1 = data.map((item, index) => {
          item.list = []
          item.page = 0
          item.pagesize = 10
          item.finished = false
          item.loading = false
          return item
        })
        this.category = category1
        this.selectArticle()
      },
      // 根据页码请求数据
      async selectArticle() {
        const categoryitem = this.categoryItem()
        const res = await this.$http.get('/detail/' + categoryitem._id, {
          params: {
            page: categoryitem.page,
            pagesize: categoryitem.pagesize
          }
        })  
        /* console.log(res) */
        categoryitem.list.push(...res.data)
        /* console.log(categoryitem) */
        categoryitem.loading = false
        // 判断数据是否全部加载完毕
        if (res.data.length < categoryitem.pagesize) {
          categoryitem.finished = true
        }
      },
      // 获取当前页码
      categoryItem() {
        const categoryitem = this.category[this.active]
        return categoryitem
      },
      onLoad() {
        /* console.log('已经到底部了') */
        const categoryitem = this.categoryItem()
        /* 通过setTimeout设置加载时间 */
        /* setTimeout(() => {
          categoryitem.page += 1
          this.selectArticle()
        }, 1000) */
        categoryitem.page += 1
        this.selectArticle()
      }
    },
    // 监测active变化，实时更新页面信息
    watch: {
      active() {
        this.selectArticle()
      }
    },
    created() {
      this.selectCategory()
    }
}
</script>

<style scoped>
.home{
  background-color: #fff;
}
.cover-video{
  width: 50%;
  display: inline-block;
}
</style>