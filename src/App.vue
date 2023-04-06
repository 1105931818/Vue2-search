<template>

    <div class="main">
        <Search/>
        <List/>
    </div>

</template>


<script>

    //引入组件"
    import Search from './components/Search.vue';
    import List from './components/List.vue';
    export default {
        name:"App",
        data() {
            return {
                
            }
        },
        components:{
            Search,
            List
        },
    }

</script>

<style scoped lang="less">

    .main{
        width: 1200px;
        margin: auto;
        background-color: cornsilk;
    }

</style>