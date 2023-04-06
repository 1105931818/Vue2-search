<template>
    <div class="main1">
        <h1>Search Github Users</h1>
        <div class="search">
            <input type="text" placeholder="enter the name you search" v-model="inp">
            <button @click="getGithub">Search</button>
        </div>
    </div>
</template>

<script>

    import axios from "axios"

    export default {
        name:"SearchS",
        data() {
            return {
                inp:""
            }
        },
        methods:{
            getGithub(){
                if(!this.inp.trim()){
                    this.inp = ""
                    return alert("输入不能为空")
                }

                this.$bus.$emit("getgithub" , {isFirst:false , isLoading:true  , githubs:[]})

                axios.defaults.baseURL = "https://api.github.com/search"
                axios.get(`users?q=${this.inp}`)
                .then(response => {
                    console.log("请求成功了")
                    this.$bus.$emit("getgithub" , {isLoading:false ,  githubs:response.data.items})
                    },error =>{
                        this.$bus.$emit("getgithub" , {isLoading:false , errMsg:error.message , githubs:[]})
                        return alert("请求失败")
                    }
                )
            }
        }
    }
</script>

<style scoped lang="less">
    .main1{
        width: 850px;
        height: 200px;
        margin: auto;
        background-color: darkslategrey;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: center;

        .search{
            width: 510px;
            height: 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;

            input{
                width: 400px;
                height: 34px;
                font-size: 16px;
                outline: none;
                border-radius: 4px;
                border: none;

                &::-webkit-input-placeholder{
                    font-size: 16px;
                    color: darkslategray;
                }
            }

            button{
                width: 100px;
                height: 36px;
                color: darkslategray;
                border-radius: 4px;
                border: none;
            }
        }
    }
</style>