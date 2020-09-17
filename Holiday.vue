<template>
    <div class="hod">
        <div class="header" fixed>
            <router-link to="/">
                <mt-header title="旅游度假 · 北京站">       
                    <mt-button slot="left" icon="back"></mt-button>
                    <mt-button slot="right" icon="more"></mt-button>
                </mt-header>
                
            </router-link>
            <!-- 顶部搜索 -->
            <!-- <router-link to="/"> -->
                <!-- <mt-search v-model="value" cancel="取消" placeholder="搜索目的地"></mt-search> -->
                <!-- <div class="search_header">
                    <img src="../assets/image/search.png" alt="">
                    <input type="text" placeholder="搜索目的地">
                </div> -->
            <!-- </router-link> -->
        </div>
        <!-- 轮播图开始 -->
        <div style="height:100px">
            <mt-swipe :auto="4000">
                <mt-swipe-item><img src="../assets/image/banner1.png" class="center_photo"></mt-swipe-item>
                <mt-swipe-item><img src="../assets/image/banner2.png" class="center_photo"></mt-swipe-item>
                <mt-swipe-item><img src="../assets/image/banner3.png" class="center_photo"></mt-swipe-item>
            </mt-swipe>
        </div>
        <!-- 轮播图结束 -->
        <!-- 目的地开始 -->
        <h4>当季热门目的地</h4>     
            <div class="bg">
            <div v-for="(item,i) of list" :key="i" class="bg_1">     
                <router-link :to="'/list/'+item.id">
                    <div class="bg_2">
                        <img :src="item.image" alt="">
                        <p class="bg_3">{{item.text}} <br>{{item.tet}}</p>
                    </div> 
                </router-link>
            </div>
        </div>
        <!-- 目的地结束 -->
        <!-- 选择地点开始 -->
        <div class="btn1">
            <div v-for="(elem,i) of 8" :key="i">
                <mt-button type="primary" plain size="small" class="btn2">张家界</mt-button>
            </div>
        </div>
        <!-- 选择地点结束 -->
        <div class="photo_center">
            <div>
                <img src="../assets/image/bottom1.png" alt="">
            </div>
            <div>
                <img src="../assets/image/bottom2.png" alt="">
            </div>
            <div>
                <img src="../assets/image/bottom3.png" alt="">
            </div>
            <div>
                <img src="../assets/image/bottom4.png" alt="">
            </div>
        </div>
        <div class="bottom">
            <div v-for="(item,i) of 12" :key="i">
                <img src="../assets/image/bottom_bottom1.png" alt="">
                <p>周边游</p>
            </div>
        </div>
        <!-- 选项卡开始 -->
        <mt-navbar v-model="active">
            <mt-tab-item id="1">
                <p>尾单特惠</p>
            </mt-tab-item>
            <mt-tab-item id="2">
                <p>低价预售</p>
            </mt-tab-item>
            <mt-tab-item id="3">
                <p>超值自由行</p>
            </mt-tab-item>
        </mt-navbar>
        <!-- 选项卡结束 -->
        <!-- 面板区域开始 -->
        <mt-tab-container v-model="active">
            <mt-tab-container-item id="1" class="bottom_travel">
                <div class="bottom_travel_div"  v-for="(item,i) of 6" :key="i">
                    <img src="../assets/image/bottom_photo1.png" alt="">
                    <p>6人VIP小团随走随停，超火青甘大环线8日游，西宁进出，赠沙漠露营</p>
                    <div class="price">¥3607起/人</div>
                </div>
            </mt-tab-container-item>
             <mt-tab-container-item id="2" class="bottom_travel">
               <div  class="bottom_travel_div" v-for="(item,i) of 6" :key="i">
                    <img src="../assets/image/bottom_photo10.png" alt="">
                    <p>6人VIP小团随走随停，超火青甘大环线8日游，西宁进出，赠沙漠露营</p>
                    <div class="price">¥3607起/人</div>
                </div>
            </mt-tab-container-item>
             <mt-tab-container-item id="3" class="bottom_travel">
                <div  class="bottom_travel_div" v-for="(item,i) of 6" :key="i">
                    <img src="../assets/image/bottom_photo9.png" alt="">
                    <p>6人VIP小团随走随停，超火青甘大环线8日游，西宁进出，赠沙漠露营</p>
                    <div class="price">¥3607起/人</div>
                </div>
            </mt-tab-container-item>
        </mt-tab-container>
        <!-- 面板区域结束 -->
        <!-- 底部选项卡开始 -->
        <mt-tabbar v-model="select" class="mt_bottom" fixed>
            <mt-tab-item id="holiday">
                <img src="../assets/image/holiday.png" alt="" slot="icon">
                度假
            </mt-tab-item>
             <mt-tab-item id="good shape">
                <img src="../assets/image/price.png" alt="" slot="icon">
                好货
            </mt-tab-item>
             <mt-tab-item id="price">
                <img src="../assets/image/good shape.png" alt="" slot="icon">
                特卖
            </mt-tab-item>
             <mt-tab-item id="my">
                <img src="../assets/image/my.png" alt="" slot="icon">
                我的
            </mt-tab-item>
        </mt-tabbar>
        <!-- 底部选项卡结束 -->
    </div>
</template>



<script>
export default {
    data(){
        return{
            active:"1",
            select:"holiday",
            photo:[
                {id:1,text:"丽江",tet:"796人喜欢",image:"center_photo1.png"},
                {id:2,text:"三亚",tet:"796人喜欢",image:"center_photo2.png"},
                {id:3,text:"桂林",tet:"796人喜欢",image:"center_photo3.png"},
                {id:4,text:"普吉岛",tet:"796人喜欢",image:"center_photo4.png"},
                {id:5,text:"芽庄",tet:"796人喜欢",image:"center_photo5.png"},
                {id:6,text:"巴厘岛",tet:"796人喜欢",image:"center_photo6.png"}
            ],
            list:[]
            }
    },
    mounted(){
        this.photo.forEach(item=>{
            if(item.image!=null){
                item.image=require("../assets/image/" +item.image)
            }
            // console.log(item)
            this.list.push(item);
        })
        // console.log(this.list);
    }
}
</script>

<style>
    /* 顶部样式 */
    .hod .header{
    background-color: #ef4f4f;
    padding-bottom: 5px;
    margin-bottom: 10px;
    }
    /* 搜索框样式 */
    .hod .search_header{
        width: 352px;
        height: 20px;
        display: block;
        margin: 0 auto;
        border: 1px solid #000;
        border-top-right-radius: 15px;
        border-top-left-radius: 15px;
        border-bottom-right-radius: 15px;
        border-bottom-left-radius: 15px;
        padding: 5px;
        background-color: #fff;
    }
    .hod .search_header input{
        border: 1px solid #fff;
    }
    /* 轮播图样式 */
    .hod .center_photo{
        width: 100%;
    }
    /* 面板样式 */
    .hod .bg{
        position: relative;
        display: flex;
        flex-wrap: wrap;
        box-sizing: border-box;
        justify-content: space-around;
    }
    .hod .bg_1{
        position: relative;
        width: 32%;
    }
    .hod .bg img{
        width: 100%;  
    }
    .hod .bg_1 .bg_3{
        position: absolute;
    }
    .hod .bg_3{
        width: 50%;
        height: 50%;
        text-align: center;
        position: absolute;
        top:3.5rem;
        left: 2rem;
        font-size: 12px;
        color: #fff;
        background-color:rgb(255, 255, 255,.6);
    }
    /* 中部地点连接 */
    .hod .btn1{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        margin-bottom: 1rem;
        /* border: 1px solid #000; */
        padding-bottom: 1rem;
    }
    .hod .btn2{
        margin-right: .9rem;
        border: 1px solid rgb(218, 208, 208) !important;
        margin-top: 1rem;
    }
    /* 底部照片 */
    .hod .photo_center{
        display: flex;
        box-sizing: border-box;
        justify-content: space-around;
    }
    .hod .photo_center img{
        width: 100%;
    }
    .hod .bottom{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 1rem;
    }
    .hod .bottom div{
        width: 16%;
        text-align: center; 
    }
    .hod .bottom p{ 
        font-size: 0.5rem;
        margin-top: -0.5rem;
    }
    /* 底部导航 */
    .bottom_travel{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
    }
    .bottom_travel_div{
        width: 48%;
        margin: 1rem 0;
    }
    .bottom_travel_div{
        font-size: 14px;
    }
    .bottom_travel_div img{
        max-width: 100%;
    }
    /* 底部选项卡 */
    .mt_bottom{
        background-color: #fafafa;
    }
    .price{
        color:#ff8300;
        font-size: 16px;
        font-weight: bold;
    }
</style>