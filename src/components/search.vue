<template>
    <div class="mysearch">
        <div class="logo">
            <img src="./../assets/baidu_logo.png" alt="">
        </div>
        <div class="search-input">
            <input type="text">
            <span class="search-reset" @click="clearInput()">&times;</span>
            <button class="search-btn" @click="search()">百度一下</button>
            <!-- 显示下拉数据 -->
            <div class="search-select">

            </div>
        </div>
    </div>
</template>
<script>
    
</script>
<style lang='stylus' scoped>
    .mysearch
        // background red
        .search-input
            width 600px
            height 45px
            // background green
            margin 0 auto
            margin-top 10px
            position relative
            input 
                float left
                border 1px solid #e4e4e4
                box-sizing border-box
                width 500px
                height 45px
                padding-left 10px
                font-size 18px
                overflow 
                outline none
            .search-reset
                position absolute
                top 14px
                right 110px
            .search-btn
                float left
                width 100px
                height 45px
                border 1px solid #3385ff
                background #3385ff
                font-size 16px
                color #ffffff
                font-weight bold
</style>
