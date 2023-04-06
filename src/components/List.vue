<template>
    <div class="main2">
        <!-- 展示用户列表 -->
        <div class="cont" 
            v-show="info.githubs.length"
            v-for="(github) in info.githubs"
            :key="github.login">
            <a :href="github.html_url">
                <img :src="github.avatar_url" alt="">
            </a>
            <p>{{ github.login }}</p>
        </div>
        <!-- 展示初始界面 -->
        <h1 v-show="info.isFirst">欢迎使用</h1>

        <!-- 展示加载界面 -->
        <h1 v-show="info.isLoading">加载中.....</h1>

        <!-- 展示错误信息 -->
        <h1 v-show="info.errMeg">{{ info.errMeg }}</h1>
    </div>
</template>

<script>

    export default {
        name:"ListL",
        data() {
            return {
                info:{
                    isFirst:true,
                    isLoading:false,
                    errMeg:"",
                    githubs:[]
                }
            }
        },
        mounted(){
            this.$bus.$on("getgithub" , (dataObj) => {
                this.info = {...this.info , ...dataObj}
            })
        }
    }

</script>

<style scoped lang="less">

    .main2{
        width: 850px;
        margin: auto;
        background-color: darkslategray;
        margin-top: 30px;
        padding:25px 20px;
        box-sizing: border-box;
        display: flex;
        flex-wrap: wrap;
        justify-content:space-between;

        .cont{
            width: 120px;
            height: 145px;
            background-color: antiquewhite;
            padding: 10px;
            margin:0 5px;
            margin-bottom: 25px;
            box-sizing: border-box;
            border-radius: 4px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;

            a{
                flex: 1;

                img{
                    width: 100px;
                    height: 100px;
                }
            }

            p{
                width: 100%;
                height: 20px;
                margin: 0;
                line-height: 20px;
                text-align: center;
            }
        }
    }

</style>