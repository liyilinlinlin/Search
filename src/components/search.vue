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
                <transition-group name="itenfade" tag="ul">
                    <li class="select-option select-list" :class="{selectback:index==now}" v-for="(value,index) in myData" :key="index">
                        {{value}}
                    </li>
                </transition-group>
            </div>
        </div>
    </div>
</template>
<script>
    export default{
        data(){
            return {
                myData: [],
            }
        },
        methods:{
            // 清除文本框
            clearInput:function(){

            }
        }
    }
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
            .search-select
                position absolute
                top 45px
                width 500px
                box-sizing border-box
                ul 
                    list-style none 
                    text-align left 
                    margin 0
                    padding 0
                    border-bottom 1px solid #d4d4d4
                .itemfade-enter-active,.itemfade-leave-active
                    transition all -5s
                .itemfade-enter-active,.itemfade-leave-active
                    opacity 0
                li 
                    border 1px solid #d4d4d4
                    background #ffffff
                    border-top none 
                    border-bottom none 
                    width 100%
                .select-option
                    box-sizing border-box
                    padding 7px 10px
                .select-list
                    transition all .5s
                .selectback
                    background #eeeeee
                    cursor pointer
</style>
