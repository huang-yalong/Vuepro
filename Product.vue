<template>
    <div>
        <!-- 头部开始 -->
        <div class="swipe"  v-for="(value,index) of products" :key="index">
            <mt-swipe>
                <mt-swipe-item>
                    <div class="product_header">
                        <mt-button class="back icon" slot="left"></mt-button>
                        <mt-button class="like icon" slot="right"></mt-button>
                        <mt-button class="more icon" slot="right"></mt-button>
                    </div>
                    <img class="img" :src="value.swiper_1" alt="">
                </mt-swipe-item>
                 <!-- <mt-swipe-item>
                    <div class="product_header">
                        <mt-button class="back icon" slot="left"></mt-button>
                        <mt-button class="like icon" slot="right"></mt-button>
                        <mt-button class="more icon" slot="right"></mt-button>
                    </div>
                    <img class="img" :src="value.swiper_2" alt="">
                </mt-swipe-item>
                 <mt-swipe-item>
                    <div class="product_header">
                        <mt-button class="back icon" slot="left"></mt-button>
                        <mt-button class="like icon" slot="right"></mt-button>
                        <mt-button class="more icon" slot="right"></mt-button>
                    </div>
                    <img class="img" :src="value.swiper_3" alt="">
                </mt-swipe-item> -->
            </mt-swipe>
        </div>
        <!-- 头部结束 -->
        <!-- 文本开始 -->
        <div class="content" v-for="(value,index) of products" :key="'content'+index" >
            <div><span class="yen">￥</span><span class="num">{{value.price}}</span><span class="pre">起/人</span></div>
            <div class="content_text">{{value.subject}}</div>
            <div class="content_detail">暑期大促·进行中！￥350店铺联盟券随心领，更可瓜分1亿旅行金，叠加使用！旅行金最高立减￥99</div>
        </div>
        <!-- 文本结束 -->
        <!-- 详情图片开始 -->
         <!-- <div class="product_img" v-for="(value,index) of products" :key="'product_img'+index">
           <div v-html="value.content">
                
            </div> 
        </div> -->
        <div class="discuss">
        <div>
            <textarea name="tar" id="tar" cols="30" rows="10"></textarea>
            <span @click="send" class="send">发布</span>
        </div>
        <div class="discuss-item" v-for="(item,index) of results" :key="index">
            <div class="left">
                <img src="../assets/user/timg.jpg">
            </div>
            <div class="right">
                <p class="tt">
                    <span class="tl">{{username}}</span>
                    <span class="tr" @click="assist1(index)">
                            {{item.assist}}
                        <img src="../assets/user/zan.png">
                    </span>
                </p>
                <div class="tm">
                    {{item.content}}
                </div>
                <div class="time">
                    <span class="time1">
                        {{item.time}}
                    </span>
                </div>
            </div>
        </div>
    </div>
        <!-- 详情图片结束 -->
        <!-- 底部导航开始 -->
        <div class="product_bottom">
            <div class="product_bottom_nav">
                <div class="icon-item">
                     <!-- <router-link :to="'/cart/'+id"> -->
                     <router-link :to="'/lianxi/'+id">
                        <img src="/img/cart.png">
                    </router-link> 
                        <span>购物车</span>
                </div>
            </div>
            <div class="btn">
                <!-- <a class="item item-l" href="#">加入购物车</a> -->
                <router-link class="item item-r" :to="'/lianxi/'+id">加入购物车</router-link>
                <!-- <a class="item item-r" href="#">立即预定</a> -->
            </div>
        </div>
        <!-- 底部导航结束 -->
    </div>
</template>
<script>
export default {
    data(){
        return {
            products:[],
            id:1,

            assist:0,
            pid:1,
            author:1,
            time:"",
            results:"",
            username:""
        }
    },
    methods:{
         assist1(index){
            // this.assist+=1;
             this.axios.post('/upd','aid='+this.results[index].id).then(res=>{
                // console.log(res.data.message);
            })
            this.axios.post('/upd','aid='+this.results[index].id).then(res=>{

                    this.assist=res.data.results[0].assist;
                    
                    // console.log(this.assist);
            })
        },
        send(){
            let mNow=new Date().getMonth() ? "0"+Number(new Date().getMonth()+1):Number(new Date().getMonth()+1);
            let dNow=new Date().getDate();
            let hNow=new Date().getHours();
            let MinNow=new Date().getMinutes();
            let content=document.getElementById("tar");
            content=content.value;
            this.time=this.time+mNow+"-"+dNow+" "+hNow+":"+MinNow;
            this.axios.post('/assist','time='+this.time+'&assist='+this.assist+'&pid='+this.pid+'&content='+content+'&author='+this.author).then(res=>
        {
            console.log(res.data.message);
        });
        }
    },
    mounted(){
        // this.id=sessionStorage.getItem('userId');
        // console.log(this.id);
        this.id=this.$route.params.id;
        console.log(this.id);
        this.axios.get('/product?id='+this.id).then(res=>{
            let data=res.data.results;
            // console.log(data);
              data.swiper_1=require('../assets/image/'+data.swiper_1);
              this.products.push(data);
             
        });




        this.username=sessionStorage.getItem("username");
      this.axios.get('/assist?pid='+this.pid).then(res=>{
        //   this.results=res.data.results;
        //    console.log(this.results);
        let data=res.data.results;
        data.forEach(item => {
            if(item.content!=null){
                sessionStorage.setItem('content',item.content);
            }
        });
        this.results=data;
      });
    }
}
</script>
<style scoped>
    *{margin: 0;padding: 0;}
    .icon-item img{
        width: 28px;
    }
    .icon-item span{
        font-size: 12px;
    }
    .icon-item{
        /* width: 36px; */
        height: 49px;
        /* line-height:49px; */
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    /* .product_header{
        position: relative;
    } */
    .swipe{height: 240px;}
    .img{
        max-width: 100%;
    }
    .icon{
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }
    .back{
        background: url('../assets/image/back.png') rgba(0,0, 0,.4) no-repeat center;
        background-size: 60%;
        position: absolute;
        left: 0px;
        top: 0px;
    }
    .like{
        background: url('../assets/image/like.png') rgba(0,0, 0,.4) no-repeat center;
        background-size: 60%;
        position: absolute;
        right: 50px;
        top: 0px;
    }
    .more{
        background: url('../assets/image/more.png') rgba(0,0, 0,.4) no-repeat center;
        background-size: 70%;
        position: absolute;
        right: 0px;
        top: 0;
    }
    .content{
        margin: 20px 0;
    }
    .content .yen{
        color: orange;
        font-size: 14px;
    }
    .content .num{
        color: orange;
        font-size: 20px;
    }
    .content .pre{
        color: #666;
        font-size: 12px;
    }
    .content .content_text{
        font-size: 20px;
        margin-top: 10px;
    }
    .content .content_detail{
        color: #999;
        font-size: 13px;
        margin-top: 10px;
    }
    .product_img img{
        max-width: 100%;
    }
    .product_bottom{
        position: fixed;
        background-color:#fff;
        height: 49px;
        left: 0px;
        bottom: 0px;
        width: 100%;
        display: flex;
    }
    .product_bottom_nav{
        width: 196px;
        height: 100%;
        /* background-color: yellow; */
    }
    .btn{
        width: 51%;
    }
    .item{
        float: left;
        width: 45%;
        height: 100%;
        line-height: 49px;
        text-decoration: none;
        margin-right: 8px;
        text-align: center;
        border-radius: 5px;
        }
    .item-l{
        background-color: #ff9800;
    }
    .item-r{
        background-image: linear-gradient(-135deg,#ff8300 0,#ff5800 100%); 
    }



     a{
        color: #333;
        text-decoration: none;
    }
    #top{
        width: 100%;
        height: 100px;
        outline: 0;
    }
    .discuss{
        margin: 10px 10px 0px;
        position: relative;
    }
    .discuss .discuss-item{
        width: 100%;
        display: flex;
        margin: 10px 0;
    }
    .discuss .discuss-item .left{
        height: 100%;
    }
    .discuss .discuss-item .left img{
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }
    .discuss .discuss-item .right{
        width: 100%;
        margin-left: 4px;
    }
    .discuss .discuss-item .right .tt{
        display: flex;
        justify-content: space-between;
    }
    .discuss .discuss-item .right .tt .tl{
        color:#1f679d;
        font-size: 14px;
    }
    .discuss .discuss-item .right .tt .tr{
        font-size: 14px;
        line-height: 19px;
    }
    .discuss .discuss-item .right .tt .tr img{
        vertical-align: middle;
    }
    .discuss .discuss-item .right .tm{
        font-size: 14px;
        color: #333;
        margin: 8px 0px;
    }
    .discuss .discuss-item .right .time{
        font-size: 12px;
        margin-bottom: 10px;
    }
    .discuss .discuss-item .right .time .time2{
        margin-left: 10px;
    }
    .discuss .discuss-item .right .reply{
        background-color: #f5f5f5;
        padding: 8px;
    }
    .discuss .discuss-item .right .uu{
        font-size: 14px;
        color: #1f679d;
    }
    .discuss .discuss-item .right .ut{
        font-size: 14px;
    }
    .discuss .discuss-item .right .r-total{
        font-size: 14px;
        color: #1f679d;
        margin-top: 8px;
    }
    #tar{
        width: 80%;
        height: 50px;
        vertical-align: bottom;
        outline: none;
    }
    .send{
        margin-left: 10px;
        vertical-align: bottom;
        font-size: 14px;
    }
</style>