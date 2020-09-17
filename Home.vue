<template>
    <div>
        <!-- 顶部搜索框开始 -->
        <div class="header_search">
            <!-- 搜索图标 -->
            <div class="search_icon"></div>
            <!-- 搜索框 -->
            <div class="search">
                <input slot="left" type="text" placeholder="搜索景点门票">
            </div>
            <!-- 顶部logo -->
            <div class="header_logo"></div>
        </div>
        <!-- 顶部搜索框结束 -->
        <!-- 顶部导航开始 -->
        <div class="header_navbar">
            <!-- 酒店 -->
            <div v-for="(value,index) of hed" :key="index">
                <router-link to="/holiday">
                    <img :src="value.image" alt="">
                    <p>{{value.text}}</p>
                </router-link>
            </div>
        </div>
        <!-- 顶部导航结束 -->
        <!-- 中部导航开始 -->
        <div class="center_navbar">
            <div v-for="(item,index) of list" :key="index">
                <router-link to="/holiday">
                    <img :src="item.image" alt="">
                    <p>{{item.text}}</p>
                </router-link>
            </div>
        </div>
        <!-- 中部导航结束 -->
        <!-- 分割页 -->
        <div class="fenge">
            <h3>特惠度假</h3>
        </div>
        <!-- 中部选项卡开始 -->
        <div class="nav_border">
            <mt-navbar v-model="active">
                    <mt-tab-item id="1">
                        <p>当季热门度假</p>
                    </mt-tab-item>
                    <mt-tab-item id="2">
                        <p>今日特惠度假</p>
                    </mt-tab-item>
            </mt-navbar>
        </div>
        <!-- 中部选项卡结束 -->
        <!-- 产品列表开始 -->
        <div class="product_list">
            <mt-tab-container v-model="active">
                <!-- 面板一 -->
                <mt-tab-container-item id="1" class="list_container">
                    <div v-for="(value,index) of cont1" :key="index" class="list_one">
                        <router-link to="/login">
                            <div class="list_div">
                                <img :src="value.image" class="bottom_img" alt="">
                                <div class="list_detial">
                                    <div>{{value.detail1}}</div>
                                    <div>{{value.detail2}}</div>
                                </div>
                            </div>                        
                            <div class="list_text">{{value.text}}</div>
                            <div class="list_price">￥{{value.price}}</div>
                        </router-link>
                    </div>
                </mt-tab-container-item>
                <!-- 面板二 -->
                <mt-tab-container-item id="2" class="list_container">
                    <div v-for="(value,index) of cont2" :key="index" class="list_one">
                        <router-link to="/login">
                            <img :src="value.image" class="bottom_img" alt="">
                            <div class="list_text">{{value.text}}</div>                       
                            <div class="ticket_text">{{value.detail1}}</div>
                            <div class="list_price">￥{{value.price}}起</div>
                        </router-link>
                    </div>
                </mt-tab-container-item>
            </mt-tab-container>
        </div>
        <!-- 产品列表结束 -->
        <!-- 分割链接开始 -->
        <div class="fenge_a">
                <router-link to="/">
                    <p>更多度假优惠></p>
                </router-link>
        </div>
        <!-- 分割链接结束 -->
        <!-- 分割页 -->
        <div class="fenge">
            <h3>特惠门票</h3>
        </div>
        <!-- 门票选项卡开始 -->
        <div class="nav_border">
            <mt-navbar v-model="ticket">
                    <mt-tab-item id="dangji">
                        <p>当季景点门票</p>
                    </mt-tab-item>
                    <mt-tab-item id="tehui">
                        <p>特惠门票</p>
                    </mt-tab-item>
            </mt-navbar>
        </div>
        <!-- 门票选项卡开始 -->
        <!-- 门票列表开始 -->
        <div class="product_list">
            <mt-tab-container v-model="ticket">
                <!-- 面板一 -->
                <mt-tab-container-item id="dangji" class="list_container">
                    <div v-for="(value,index) of pro1" :key="index" class="list_one">
                        <router-link to="/login">
                            <img :src="value.image" class="bottom_img" alt="">
                            <div class="list_text">{{value.text}}</div>                       
                            <div class="ticket_text">{{value.detail}}</div>
                            <div class="list_price">￥{{value.price}}</div>
                        </router-link>
                    </div>
                </mt-tab-container-item>
                <!-- 面板二 -->
                <mt-tab-container-item id="tehui" class="list_container">
                    <div v-for="(value,index) of pro2" :key="index" class="list_one">
                        <router-link to="/login">
                            <img :src="value.image" class="bottom_img" alt="">
                            <div class="list_text">{{value.text}}</div>                       
                            <div class="ticket_text">{{value.detail}}</div>
                            <div class="list_price">￥{{value.price}}起</div>
                        </router-link>
                    </div>
                </mt-tab-container-item>
            </mt-tab-container>
        </div>
        <!-- 门票列表结束 -->
        <!-- 分割链接开始 -->
        <div class="fenge_a">
                <router-link to="/">
                    <p>更多特惠门票></p>
                </router-link>
        </div>
        <!-- 分割链接结束 -->
        <!-- 轮播图开始 -->
        <div class="slideshow">
            <mt-swipe :auto="4000">
                <mt-swipe-item>
                    <img src="image/slideshow1.png" alt="">
                </mt-swipe-item>
                <mt-swipe-item>
                    <img src="image/slideshow2.png" alt="">
                </mt-swipe-item>
                <mt-swipe-item>
                    <img src="image/slideshow3.png" alt="">
                </mt-swipe-item>
            </mt-swipe>
        </div>
        <!-- 轮播图结束 -->
        <!-- 分割字符 -->
        <div class="fenge">
            <img src="image/gonglue.png" alt="">
            <h4>旅行攻略</h4>
        </div>
        <!-- 攻略选项卡开始 -->
        <div class="nav_border">
            <mt-navbar v-model="gonglue">
                    <mt-tab-item id="qinzi">
                        <p>趣味亲子游</p>
                    </mt-tab-item>
                    <mt-tab-item id="lvpai">
                        <p>旅拍也要出大片</p>
                    </mt-tab-item>
            </mt-navbar>
        </div>
        <!-- 攻略选项卡结束 -->
        <!-- 攻略面板区域开始 -->
        <div class="product_list">
            <mt-tab-container v-model="gonglue">
                <!-- 面板一 -->
                <mt-tab-container-item id="qinzi" class="list_container">
                    <div v-for="(value,index) of pro3" :key="index" class="list_one">
                        <router-link to="/login">
                            <img :src="value.image" class="bottom_img" alt="">
                            <div class="list_text bottom_text">{{value.text}}</div> 
                        </router-link>                      
                    </div>
                </mt-tab-container-item>
                <!-- 面板二 -->
                <mt-tab-container-item id="lvpai" class="list_container">
                    <div v-for="(value,index) of pro4" :key="index" class="list_one">
                        <router-link to="/login">
                            <img :src="value.image"  class="bottom_img" alt="">
                            <div class="list_text bottom_text">{{value.text}}</div>
                        </router-link>                       
                    </div>
                </mt-tab-container-item>
            </mt-tab-container>
        </div>
        <!-- 攻略面板区域结束 -->
        <!-- 分割链接 -->
        <div class="fenge_a">
                <router-link to="/">
                    <p>更多精彩攻略></p>
                </router-link>
        </div>
        <!-- 分割链接结束 -->
        <!-- 版权开始 -->
        <div class="banquan"></div>
        <!-- 版权结束 -->
        <!-- 底部选项卡开始 -->
        <div>
            <mt-tabbar v-model="selectTab" fixed>
                <mt-tab-item id="index">
                    首页
                    <img src="image/index_enable.png" alt="" slot="icon" v-if="selectTab=='index'">
                    <img src="image/index_disable.png" alt="" slot="icon" v-else>
                </mt-tab-item>
                <mt-tab-item id="dingdan">
                    订单
                    <img src="image/dingdan_enbale.png" alt="" slot="icon" v-if="selectTab=='dingdan'">
                    <img src="image/dingdan_disable.png" alt="" slot="icon" v-else>
                </mt-tab-item>
                <mt-tab-item id="kefu">
                    客服
                    <img src="image/kefu_enable.png" alt="" slot="icon" v-if="selectTab=='kefu'">
                    <img src="image/kefu_disable.png" alt="" slot="icon" v-else>
                </mt-tab-item>
                <mt-tab-item id="me">
                    <router-link to="/me">
                        <div class="bottom_me">
                            <img src="image/me_enable.png" alt="" slot="icon" v-if="selectTab=='me'">
                            <img src="image/me_disable.png" alt="" slot="icon" v-else>
                            <p>我的</p>
                        </div>
                    </router-link>
                </mt-tab-item>
            </mt-tabbar>
        </div>
        <!-- 底部选项卡结束 -->
        
    </div>
</template>
<style scoped>
    div,p,h1,h3,h4,h5,h6,ul,li,a,span,img,input{
        margin: 0;padding: 0;
    }
    /* 顶部搜索框 */
    .header_search{
        display: flex;
        width: 100%;height: 30px;
    }
    /* 搜索图标 */
    .search_icon{
        display: block;
        width: 10%;
        height: 30px;
        background:url(../assets/image/search.png)  no-repeat center center #e1e1e1;
    }
    /* 搜索框 */
    .search{
        width: 70%;height: 30px;
        background-color: #e1e1e1;
    }
    /* 搜索输入框 */
    .search input{
        width: 100%;height: 30px;
        box-sizing: border-box;
        border-radius: 0;
        border: 0;
        background-color: #e1e1e1;
        outline: none;
        box-shadow: none;
    }
    /* 顶部logo */
    .header_logo{
        width: 8%;height: 30px;
        background: url(../assets/image/logo.png) no-repeat center #1296DB;
        border: 1px solid #666;
        border-radius: 50%;
        margin-left: 30px;
    }
    /* 顶部导航 */
    .header_navbar{
        margin-top: 10px;
        text-align: center;
        display: flex;
    }
    .header_navbar div~div{
        margin-left: 8px;
    }
    .header_navbar img{width: 80%;}
    .header_navbar a{
        font-size: 12px;
        text-decoration: none;
        color: #000;
    }
    /* 中部导航 */
    .center_navbar{
        display: flex;
        flex-wrap: wrap;
        font-size: 12px;
        justify-content: center;
        
    }
    .center_navbar div{
        width: 20%;
        text-align: center;
    }
    /* 中部导航跳转链接 */
    .center_navbar div a{
        text-decoration: none;
        color: #000;
    }
    /* 中部导航图标 */
    .center_navbar img{
        width:50%;
    }
    /* 分割字符 */
    .fenge{
        display: flex;
    }
    .fenge h4{margin: 10px;}
    .fenge img{max-width: 100%; max-height: 16px;margin-top: 13px;}
    .fenge h3{
        margin: 20px 0;
    }
    .center-navbar a{
        font-size: 16px;
    }
    /* 详情页面/门票页面/下方亲子选项卡 */
    .mint-navbar .mint-tab-item.is-selected {
        background-color:  #00A99D;
        border: 0;
        color: #fff;
        margin-bottom: 0;
    }
    .nav_border{
        border:1px solid #000;
        border-radius: 0.3rem;
    }
    /* 产品/门票列表外层 */
    .product_list{
        width: 100%;
        margin-top: 20px;
        margin-bottom: 20px;
    }
    .list_container{
        display: flex;
        flex-wrap: wrap; 
        justify-content: space-between;
    }
    .list_one{
        width: 48%;
        margin-bottom:10px ;
    } 
    /* 产品图片 */
    .list_div{
        position: relative;
        width: 100%;
    }
    /* 产品公告 */
    .list_detial{
        text-align: center;
        width: 50%;
        background-color: rgba(0, 0, 0,.5);
        position: absolute;
        bottom: 4%;
        left: 25%;
    }
    .list_detial :first-child{
        color: #fff;
        font-size: 14px;
    }
    .list_detial :last-child{
        color: yellow;
        font-size: 12px;
        margin-top: 5px;
    }
    /* 产品详情/门票标题 */
    .list_container a{
        color:#000;
        text-decoration: none;
    }
    .list_text{
        width: 100%;height: 20px;
        font-size: 14px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    /* 产品价格/门票价格 */
    .list_price{
        color: orange;
        font-size: 18px;
        font-weight: bold;
    }
    /* 分割链接 */
    .fenge_a{
        width: 80%;height: 40px;
        border: 1px solid #00A99D;
        border-radius: .5rem;
        text-align: center;
        line-height: 40px;
        margin: 0 auto;
    }
    .fenge_a a{
        color: #00A99D;
        text-decoration: none;
    }
    /* 门票面板区域的详情样式 */
    .ticket_text{
        font-size: 14px;
        color: #999;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
    }
    /* 轮播图 */
    .slideshow{
        width: 100%;height:123px;
        margin-top: 20px;
    }
    .slideshow img{width: 100%;}
    /* 攻略面板标题 */
    .bottom_text{overflow: visible;white-space: inherit;height: 30px;}
    /* 攻略面板图片 */
    .bottom_img{
        max-width: 100%;
    }
    /* 底部间距 */
    .banquan{margin: 60px 0;}
    .is-fixed{height: 2.9rem}
    .mint-tab-item-label a .bottom_me p{
        margin-top: 4px;
        color: #2c3e50;
    }
</style>
<script>
export default {
    data(){
        return{
            active:'1',
            selectTab:'index',
            ticket:'dangji',
            gonglue:'qinzi',
            header:[
                {text:'酒店',image:'hotel.png'},
                {text:'机票',image:'flight.png'},
                {text:'火车票',image:'train.png'},
                {text:'度假',image:'package.png'},
                {text:'景点门票',image:'piao.png'},
            ],
            hed:[],
            navbar:[
                {text:'海外酒店',image:'overseas hotel.png'},
                {text:'低价机票',image:'Cheap flights.png'},
                {text:'汽车票船票',image:'bus ticket.png'},
                {text:'自由行',image:'travel.png'},
                {text:'攻略',image:'strategy.png'},
                {text:'民宿客栈',image:'homestay.png'},
                {text:'专车自驾',image:'car.png'},
                {text:'赚钱.信用卡',image:'card.png'},
                {text:'旅游团购',image:'group_buying.png'},
                {text:'一日游',image:'one-day.png'},
                {text:'特惠酒店',image:'cheap_hotel.png'},
                {text:'借钱',image:'lend_money.png'},
                {text:'白金卡',image:'platinum_card.png'},
                {text:'行程设计',image:'journey.png'},
                {text:'周边短途',image:'circum.png'},
            ],
            list:[],
            content1:[
                {text:'含往返飞机票+3晚住宿',detail1:'郑州-丽江',detail2:'4天跟团游',price:3485,image:'z-s.png'},
                {text:'含往返飞机票(含税)+4晚住宿',detail1:'郑州-三亚',detail2:'5天自由行',price:2480,image:'zh-san.png'},
                {text:'含往返飞机票(含税)+3晚住宿',detail1:'郑州-重庆',detail2:'4天自由行',price:2090,image:'z-c.png'},
                {text:'含往返飞机票+5晚住宿',detail1:'郑州-泰国',detail2:'6天跟团游',price:6666,image:'z-t.png'},
            ],
            cont1:[],
            content2:[
                {text:'郑州-广州 4天自由行',detail1:'好事成双·双长隆4日！四大园区门票+接送机 2晚长隆熊猫+1晚珠海长隆横琴湾',price:3980,image:'z-guang.png'},
                {text:'郑州-广州 4天自由行',detail1:'戏耍双长隆嗨玩假期4日！四大园区门票+接送机 2晚广州长隆+1晚珠海企鹅酒店',price:3880,image:'zheng-g.png'},
                {text:'郑州-长隆旅游度假区 4天自由行',detail1:'亲子双长隆4日自由行！三园门票+接送机 1晚珠海企鹅酒店+2晚长隆熊猫酒店',price:3780,image:'z-chang.png'},
                {text:'郑州-广东 5天自由行',detail1:'亲子无极限双长隆5日！四大园区门票+企鹅自助午餐+接送机 广州长隆+珠海企鹅',price:4480,image:'zheng-guang.png'},
            ],
            cont2:[],
            product1:[
                {text:'龙门石窟',detail:'世界文化遗产 中国石刻艺术宝库',price:'125',image:'lmsk.png'},
                {text:'清明上河园',detail:'穿越宋朝，亲身体验清明上河图',price:'100',image:'qmshy.png'},
                {text:'开封银基水世界',detail:'大型文化旅游产业项目',price:'105',image:'yj.png'},
                {text:'银基冰雪世界',detail:'银基冰雪世界 全新升级 强势回归',price:'98',image:'yjbx.png'},
            ],
            pro1:[],
            product2:[
                {text:'开封银基水世界',detail:'大型文化旅游产业项目',price:'105',image:'yj.png'},
                {text:'少林寺',detail:'登顶中岳嵩山，一览天下胜景，领略禅宗教法',price:'169',image:'slc.png'},
                {text:'银基冰雪世界',detail:'银基冰雪世界 全新升级 强势回归',price:'98',image:'yjbx.png'},
                {text:'郑州方特欢乐世界',detail:'高科技主题乐园，方特成就欢乐梦想',price:'270',image:'zzft.png'},
            ],
            pro2:[],
            product3:[
                {text:'驾一叶扁舟，寻瓯江往事',image:'qinzi1.png'},
                {text:'不负嵊夏好时光，泗乎太安逸',image:'qinzi2.png'},
                {text:'探访日本，一部家庭旅行画册',image:'qinzi3.png'},
                {text:'厦门，带娃出行与幸福同行',image:'qinzi4.png'},
            ],
            pro3:[],
            product4:[
                {text:'美帝的美，留在图里也要藏在心底',image:'lvpai1.png'},
                {text:'在秘密花园，领略意大利风情',image:'lvpai2.png'},
                {text:'带着相机去旅行，圆一场青海梦',image:'lvpai3.png'},
                {text:'带着相机去旅行，圆一场青海梦',image:'lvpai4.png'},
            ],
            pro4:[],
        }
    },
    mounted(){
        function img(a,b){
            a.forEach((item)=>{
                if(item.image!=null){
                    item.image=require('../../public/img/'+item.image);
                }
                b.push(item);
            });
        }
        img(this.header,this.hed);
        img(this.navbar,this.list);
        img(this.content1,this.cont1);
        img(this.content2,this.cont2);
        img(this.product1,this.pro1);
        img(this.product2,this.pro2);
        img(this.product3,this.pro3);
        img(this.product4,this.pro4);
    }
}
</script>