<template>
  <div v-if="model" class="editViews">
      <nav-bar></nav-bar>

      <div class="uploadfile">
          <van-uploader class="uploadimg" :after-read="afterRead" preview-size="11.111vw"></van-uploader>
            <edit-banner left="头像" class="avatar">
                <img :src="model.user_img" slot="right" alt="" v-if="model.user_img">
                <img src="@/assets/default_img.jpg" slot="right" alt="" v-else>
            </edit-banner>
      </div>
      <edit-banner left="昵称" @BannerClick="show = true">
          <a href="javascript:;" slot="right">{{model.name}}</a>
      </edit-banner>
      <edit-banner left="账号">
          <a href="javascript:;" slot="right">{{model.username}}</a>
      </edit-banner>
      <edit-banner left="性别" @BannerClick="gendershow = true">
          <a href="javascript:;" slot="right">{{model.gender}}</a>
      </edit-banner>
      <edit-banner left="个性签名" @BannerClick="textshow = true">
          <a href="javascript:;" slot="right">{{model.user_desc}}</a>
      </edit-banner>

      <div class="editback sign-out" @click="signOut">退出登录</div>
      <div class="editback" @click="$router.back()">返回空间</div>

      <van-dialog 
        v-model="show" 
        title="昵称" 
        show-cancel-button 
        @confirm="confirmClick"
        @cancel="content = ''"
      >
          <van-field v-model="content" autofocus></van-field>
      </van-dialog>      
      <van-dialog 
        v-model="textshow" 
        title="个性签名" 
        show-cancel-button 
        @confirm="textareaClick"
        @cancel="content = ''"
      >
          <van-field v-model="content" autofocus type="textarea"></van-field>
      </van-dialog>
      <van-action-sheet v-model="gendershow" cancel-text="取消" :actions="actions" @select="onSelect" />
  </div>
</template>

<script>
import NavBar from '../components/common/Navbar'
import editBanner from '../components/common/editBanner'

export default {
    data() {
        return {
            model: {},
            show: false,
            textshow: false,
            gendershow: false,
            gender: '保密',
            actions: [{ name: '男',val: 0}, { name: '女' ,val:1},{ name: '保密', val:2}],
            content: ''
        }
    },
    components: {
        NavBar,
        editBanner
    },
    // TODO: 2020/6/15 给昵称和个性签名添加正则
    methods: {
        async selectUser() {
        const res = await this.$http.get('/user/' + localStorage.getItem('id'), {
            /* headers: {
            'Authorization': 'Bearer ' + localStorage.getItem('token')
            } */
        })
        this.model = res.data[0]
        /* console.log(res) */
        /* console.log(this.model) */
        },
        async afterRead(file) {
            const formdata = new FormData()
            formdata.append('file', file.file)
            /* console.log(formdata) */
            const res =  await this.$http.post('/upload', formdata)
            /* console.log(res) */
            this.model.user_img = res.data.url
            this.UserUpdate()
        },
        async UserUpdate() {
            const res = await this.$http.post('/update/' + localStorage.getItem('id'), this.model)
            if(res.data.code == 200){
                this.$msg.fail('修改成功')
            }
        },
        confirmClick() {
            /* console.log('用户点击确认了') */
            this.model.name = this.content
            this.UserUpdate()
            this.content = ''
        },
        textareaClick() {
            /* console.log(this.content) */
            this.model.user_desc = this.content
            this.UserUpdate()
            this.content = ''
        },
        onSelect(data) {
            /* console.log(data) */
            this.model.gender = data.name
            this.UserUpdate()
            this.gendershow = false
        },
        signOut() {
            localStorage.setItem('token','')
            localStorage.setItem('id','')
            this.$router.push('/login')
        }
    },
    created() {
        this.selectUser()
    }
}
</script>

<style>
.uploadfile{
    position: relative;
    margin-top: 2.778vw;
}
.uploadimg{
    position: absolute;
    top: 3.889vw;
    right: calc(4.444vw - 8px);
    opacity: 0;
}
.editViews a{
    color: #999;
}
.avatar img{
    height: 11.111vw;
    width: 11.111vw;
    border-radius: 50%;
}
.avatar span:nth-child(1){
    padding: 6.667vw 0;
}
.editback{
    padding: 3.889vw 4.444vw;
    background-color: #fff;
    text-align: center;
    font-size: 3.889vw;
    color: #505050;
    border-bottom: 1px solid #eee;
}
.sign-out{
    margin-top: 5.556vw;
}
</style>
