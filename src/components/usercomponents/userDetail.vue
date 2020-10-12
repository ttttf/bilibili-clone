<template>
    <div>
        <div class="userdetail">
            <div class="part1">
                    <div class="user-img">
                        <img :src="userInfo.user_img" alt="" v-if="userInfo.user_img">
                        <img src="@/assets/head_img.jpg" alt="" v-else>
                    </div>
                    <div class="user-edit">
                        <div class="count">
                            <p>
                                <span class="num">0</span>
                                <br>
                                <span class="user-text">粉丝</span>
                            </p>
                            <span class="spilt"></span>
                            <p>
                                <span class="num">0</span>
                                <br>
                                <span class="user-text">关注</span>
                            </p>
                            <span class="spilt"></span>
                            <p>
                                <span class="num">0</span>
                                <br>
                                <span class="user-text">获赞</span>
                            </p>
                        </div>
                        <div class="user-editBtn" @click="$router.push('/edit')">编辑资料</div>
                    </div>
            </div>
            <div class="part2">
                <h2 class="username">{{userInfo.name}}</h2>
                <br>
                <span class="signature" v-if="userInfo.user_desc">{{userInfo.user_desc}}</span>
                <span class="signature" v-else>这个人很神秘，什么都没有写</span>
            </div>       
        </div>
  </div>
</template>

<script>
export default {
    props: ['userInfo']
}
</script>

<style>
.userdetail{
    background-color: white;
    height: 44.444vw;
    padding: 0 12px;
}
.part1{
    height: 25vw;
}
.part2{
    height: 19.444vw;
}
.user-img{
    float: left;
}
.user-edit{
    float: right;
    padding-top: 2.222vw;
}
.count p{
    display: inline-block;
    width: 20vw;
    text-align: center;
    vertical-align: middle;
    padding: 0;
    margin: 0;
}
.user-img img{
    margin-top: -1.944vw;
    border-radius: 50%;
    height: 23.611vw;
    width: 23.611vw;
}
.spilt{
    width: 1px;
    background-color: #e7e7e7;
    height: 3.889vw;
    vertical-align: middle;
    display: inline-block;
}
.num{
    font-size: 3.889vw;
    color: #212121;
    line-height: 4.444vw;
}
.user-text{
    font-size: 3.333vw;
    color: #999;
}
.user-editBtn{
    background-color: #fff;
    border: 1px solid #fb7299;
    color: #fb7299;
    width: 100%;
    display: block;
    height: 6.667vw;
    font-size: 3.333vw;
    border-radius: 0.833vw;
    margin-top: 2.778vw;
    text-align: center;
    line-height: 6.667vw;
}
.username{
    color: #212121;
    font-size: 5vw;
}
.signature{
    color: #999;
    font-size: 3.611vw;
    margin-top: 2.222vw;
}
</style>
