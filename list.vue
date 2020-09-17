<template>
    <div class="list">
        <mt-header type="primary">
            <router-link to="/" slot="left">
                <mt-button icon="back"></mt-button>
            </router-link>
            <router-link to="/" slot="right">
                <mt-button icon="more"></mt-button>
            </router-link>
        </mt-header>
        <div class="list-item"
         infinite-scroll-distance="10"
         v-infinite-scroll="loadMore"
         infinite-scroll-disabled="busy"
         infinite-scroll-immediate-check="true"
        >
            <div class="item" v-for="(item,index) of list" :key="index">
                <div class="a1">
                     <div class="item-tit" :style="{'backgroundImage':'url('+item.image+')'}" v-lazy:background-image="item.image">
                        <div class="tag">
                            <span class="tag-text">
                                <!-- 交通·酒店·定制 -->
                                {{item.tag}}
                            </span>
                        </div>
                    </div>
                </div>
                <div class="item-cont">
                    <h5 class="title">
                        <router-link :to="'/product/'+item.id">
                            <span>
                            <!-- 桂林阳朔北海银滩三亚9日🔥5星海景房蜈支洲岛+漓江游船+世外桃源呀诺达南山 -->
                                {{item.subject}}
                            </span>
                        </router-link>
                    </h5>
                    <div class="container">
                        <p class="desc">
                            <span>9天8晚</span>
                            <span class="vertical-line">|</span>
                            <span>国庆</span>
                            <span class="vertical-line">|</span>
                            <span>中国国际航空直飞</span>
                        </p>
                        <p class="desc">
                            <span class="score">
                                <span>10.0</span>
                                <span>分</span>
                            </span>
                            <span class="vertical-line">|</span>
                            <span class="normal">已售246人</span>
                        </p>
                    </div>
                    <div class="price">
                        <div class="sales-tag">
                            <span>
                                <span class="yen">￥</span>
                                <span class="num"><!--2985-->{{item.price}}</span>
                                <span class="at-least">起/人</span>
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            active:1,
            list:[],
            busy:false,
            page:1,
            pagecount:0
        }
    },
    methods:{
        loadMore(){ 
            this.page++;
            this.active=this.$route.params.id;
            if(this.page<=this.pagecount){
                this.busy=true;
                this.$indicator.open('加载中...');
                this.axios.get('/list?lid='+this.active+'&page='+this.page).then(res=>{
                 let data=res.data.results;
                 this.pagecount=res.data.pagecount;
                 data.forEach(item => {
                     if(item.image!=null){
                          item.image=require('../assets/image/'+item.image);
                        }
                     // console.log(item.image);
                     this.list.push(item);
                 });
                 this.busy=false;
                 this.$indicator.close();
              });
              
            }
        }
    },
    mounted(){
        this.active=this.$route.params.id;
        this.axios.get('/list?lid='+this.active+'&page='+this.page).then(res=>{
            // console.log(res.data.results);
            let data=res.data.results;
            this.pagecount=res.data.pagecount;
            // console.log(data);
            data.forEach(item => {
                if(item.image!=null){
                    item.image=require('../assets/image/'+item.image);
                }
                // console.log(item.image);
                this.list.push(item);
            });
        })
    }
}
</script>

<style scoped>
a{
    text-decoration: none;
    color: #212121;
}
.a1{
    width: 110px;
    margin-right: 10px;
}
    
    .list .list-item .item{
        height: 140px;
        padding: 7px 10px;
        display: flex;
        position: relative;
        align-items: center;
    }
    .list .list-item .item .item-tit{
        /* width: 232px; */
        width: 110px;
        height: 117px;
        margin-right: 10px;
        /* background-image: url('../assets/df70ea96-a527-455b-98ec-81e9e041ea4b.jpg_480x320x90_60f6892a (2).jpg'); */
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center center;
        background-clip: padding-box !important;
    }
    .list .list-item .item .item-tit .tag{
        position: absolute;
        color: #fff;
        min-width: 60px;
        max-width: 100%; 
        height: 18px;
        font-size: 18px;
        text-align: center;
        left: 10px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        background-color:rgba(0, 0,0, 0.3);
        line-height: 15px;
        padding:0 3px;
    }
    .list .list-item .item .item-tit .tag .tag-text{
        font-size: 12px;
        
    }
    .list .list-item .item .item-cont{
        height: 126.5px;
        /* width: 67%; */
    }
    .list .list-item .item .item-cont .title{
        margin-bottom:4px;
        font-size: 14px;
        color: #212121;
        height: 40px;
        margin-top: 0px;
        font-weight: 700px;
        line-height: 20px;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
    }
     .list .list-item .item .item-cont .container{
        min-height: 42px;
        /* padding-top: 15px; */
    } 
    .list .list-item .item .item-cont .container .vertical-line{
        padding: 0 5px;
        color: #ddd;
        font-size: 12px;
    } 
    .list .list-item .item .item-cont .container .desc{
        font-size: 12px;
        margin: 0px;
    } 
    .list .list-item .item .item-cont .price{
        height: 25px;
    }
    .list .list-item .item .item-cont .price .sales-tag{
        height: 24px;
        line-height: 24px;
    }
    .list .list-item .item .item-cont .price .sales-tag .yen{
        font-size: 10px;
        color: #f60;
    }
    .list .list-item .item .item-cont .price .sales-tag .num{
        font-size: 10px;
        color: #f60;
    }
    .list .list-item .item .item-cont .price .sales-tag .at-least{
         font-size: 10px;
        color: #f60;
    }
</style>




