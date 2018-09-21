<template>
    <div class="mysearch">
        <div class="logo">
            <img src="./../assets/baidu_logo.png" alt="">
        </div>
        <div class="search-input">
            <input type="text" v-model="keyword" @keyup="get($event)" @keydown.enter="search()" @keydown.down='selectdown()' @keydown.up='selectup()'>
            <span class="search-reset" @click="clearInput()">&times;</span>
            <button class="search-btn" @click="search()">百度一下</button>
            <!-- 显示下拉数据 -->
            <div class="search-select">
                <transition-group name="itenfade" tag="ul" :class="{haveUl:ishave}">
                    <li class="select-option select-list" :class="{selectback:index==now}" v-for="(value,index) in myData" :key="index" @mouseover="selectHover(index)" @click="selectClick(index)">
                        {{value}}
                    </li>
                </transition-group>
            </div>
        </div>
    </div>
</template>
<script>
import jsonp from 'jsonp'
    export default{
        data(){
            return {
                myData: [],
                keyword: '',
                now: -1,
                ishave: false,
            }
        },
        methods:{
            // 按键获取下拉列表，
            get:function(event){
                console.log(this.keyword)
                if(event.keyCode == 38 || event.keyCode == 40){
                    return
                }
                jsonp('https://sug.so.360.cn/suggest?word=' + this.keyword + '&encodein=utf-8&encodeout=utf-8',null,(err,data)=>{
                    if(data.s != null){
                        this.ishave = true
                        this.myData = data.s
                    }
                })
            },
            //按 下键
            selectdown:function(){
                this.now++
                if(this.now == this.myData.length){
                    this.now = 0
                }
                this.keyword = this.myData[this.now]
            },
            // 按 上键
            selectup:function(){
                if(this.now <= 0){
                    this.now = this.myData.length
                }
                this.now--
                this.keyword = this.myData[this.now]
            },

            // 清除文本框
            clearInput:function(){
                console.log(this.keyword)
                this.keyword = ''
                this.myData = []
                this.ishave = false
                console.log(this.keyword)
            },
            search:function(){
                window.open('https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=0&rsv_idx=1&tn=baidu&wd='+this.keyword)
            },
            selectHover(index){
                this.now = index
            },
            selectClick(index){
                this.keyword = this.myData[index]
                this.search()
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
            :focus
                outline none
            .search-reset
                position absolute
                top 14px
                right 110px
                cursor pointer
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
                    // border-bottom 1px solid #d4d4d4
                    margin-bottom 10px
                .haveUl
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
