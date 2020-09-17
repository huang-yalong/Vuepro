<template>
    <div class="parent">
        <!-- 头部开始 -->
        <div class="me_header">
            <div>
                <router-link to="/" slot="left">
                    <mt-button icon="back"></mt-button>
                </router-link>
            </div>
            <div class="me_avatar">
                <div class="fff">
                    <div class="me_header_avatar" :style="{'backgroundImage':'url(user/'+image+')'}"></div>
                    <router-link to="/login">登录 </router-link>/
                    <router-link to="/register">注册</router-link>
                    
                </div>
            </div>
        </div>
        <!-- 头部结束 -->
        <!-- 钱包面板开始 -->
        <div class="wallet">
            <mt-tab-container-item>
                <!-- 钱包 -->
                <div class="wallet_item">
                    <div class="wallet_img">
                        <img src="../assets/image/wallet.png" alt="">
                    </div>
                    <div class="wallet_text">我的钱包</div>
                </div>
                <!-- 余额 -->
                <div class="balance_item">
                    <router-link to="/login">
                        <p>0.00</p>
                        <p>账户余额</p>
                    </router-link>
                    <router-link to="/login">
                        <p>0</p>
                        <p>星券</p>
                    </router-link>
                    <router-link to="/login">
                        <p>0</p>
                        <p>银行卡</p>
                    </router-link>
                </div>
            </mt-tab-container-item>
        </div>
        <!-- 钱包面板结束 -->
        <!-- 订单面板开始 -->
        <div class="order">
            <mt-tab-container-item>
                <div class="order_item" v-for="(value,index) of 4" :key="index">
                    <router-link to="/login">
                        <div class="order_img">
                            <img src="../assets/image/dingdan_disable.png" alt="">
                        </div>
                        <div class="order_text">我的订单</div>
                        <div class="order_icon">></div>
                    </router-link>
                </div>
            </mt-tab-container-item>
        </div>
        <!-- 订单面板结束 -->
        <!-- 意见反馈面板开始 -->
        <div class="order">
            <mt-tab-container-item>
                <div class="order_item" v-for="(value,index) of 2" :key="index">
                    <router-link to="/login">
                        <div class="order_img">
                            <img src="../assets/image/message.png" alt="">
                        </div>
                        <div class="order_text">意见反馈</div>
                        <div class="order_icon">></div>
                    </router-link>
                </div>
            </mt-tab-container-item>
        </div>
        <!-- 意见反馈面板结束 -->
    </div>
</template>
<script>
export default {
   data(){
     return {
         image:''
     }  
   },
   mounted(){
       this.image=sessionStorage.getItem('image');
   }
}
</script>

<style scoped>
.parent .fff a{
    font-size: 12px;
    text-decoration: none;
    color: #fff;
}
.parent .fff{
    position: relative;
    margin: 0 auto;
    text-align: center;
    width: 70px;
    height: 101px;
}
.parent .ffe{
    width: 66px;
    height: 66px;
    position: absolute;
    top: 1px;
    left: 3px;
    opacity: 0;
}
    .parent{background-color: #eee;}
    /* 头部开始 */
    .me_header{
        background: url(../assets/image/mebg.png) bottom center;
        background-size: 100%;
        width: 100%;height: 10rem;
    }
    /* 头部返回按钮 */
    .mint-button{
        background-color: rgba(0,0,0,0);
        box-shadow: none;
    }
    /* 头部按钮颜色 */
    .mint-button--default{color: #fff;}
    /* 头部头像样式 */
    .me_header_avatar{
        width: 4.5rem;height: 4.5rem;
        border: .2rem solid #95B7E2;
        border-radius: 50%;
        /* background: url(../assets/image/avatar.png) ; */
        background-size: 100%;
        margin: 0 auto;
        margin-bottom: .5rem;
    }
    /* 头部文字 */
    .me_avatar a+a{
        /* margin-left: 41%; */
        font-size: 12px;
        color: #fff;
        text-decoration: none;
    }
    /* 钱包面板外层 */
    .wallet{
        background-color: #fff;
        margin-top: .6rem;
    }
    /* 钱包面板 */
    .wallet_item{
        background-color: #fff;
        padding:.5rem 0 .5rem .5rem;
        display: flex;
        border-bottom: 1px solid #eee;
    }
    /* 钱包/订单图标 */
    .wallet_img,.order_item a .order_img{
        width: 8%;height: 1.6rem;
        border-radius: .5rem;
        background-color: orangered;
        text-align: center;
    }
    /* 钱包/订单文字 */
    .wallet_text,.order_item a .order_text{
        margin:.1rem 0 0 .5rem;
        font-weight: bold;
    }
    /* 余额面板 */
    .balance_item{
        display: flex;
        justify-content: space-around;
        text-align: center;
        font-size: 1rem;
    }
    /* 余额文字 */
    .balance_item a{color: #999;text-decoration: none;}
    /* 订单面板外层 */
    .order{
        margin-top: .8rem;
        background-color: #fff;
    }
    /* 订单面板 */
    .order_item a{
        display: flex;
        color: #333;
        width: 100%;
        margin:0 0 0 .5rem;
        box-sizing: border-box;
        padding: .6rem 0;
        border-bottom: 1px solid #eee;
        text-decoration: none;
    }
    /* 订单箭头 */
    .order_item a .order_icon{
        color: #999;
        margin: .2rem 0 0 65%;
        font-weight: bold;
    }
</style>