<template>
    <div class="cart">
        <mt-header type="primary">
            <router-link to="/" slot="left">
                <mt-button icon="back"></mt-button>
            </router-link>
            <router-link to="/" slot="right">
                <mt-button icon="more"></mt-button>
            </router-link>
        </mt-header>
        <div class="goods-item" v-for="(item,index) of carts" :key="index">
            <div class="goods-tap">
                <div class="goods-left">
                    <div class="goods-img">
                        <img :src="item.image">
                    </div>
                </div>
                <div class="goods-info">
                    <p class="goods-desc">
                        <!-- 昆明大理丽江香格里拉/泸沽湖高品游丨雪山登顶+私人游艇+藏地探秘+秘境女儿国 -->
                        {{item.subject}}
                    </p>
                    <div class="goods-add-info">
                        <span class="setoff-time">{{moment.unix(item.created_at).format('Y年MM月DD日HH:mm:ss')}}出发</span>
                        <span class="setoff-person-num">{{item.adult}}成人 {{item.children}}儿童</span>
                    </div>
                    <div class="goods-price">
                        <span class="goods-price-ico">￥</span>
                        <span class="goods-price-num">{{item.price}}</span>
                        <span>起</span>
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
            carts:[],
            uid:2,
        }
    },
    mounted(){
        // this.uid=this.$route.params.uid;
        this.uid=sessionStorage.getItem('userId');                                             
        this.axios.get('/cart?uid='+this.uid).then(res=>{
            // console.log(res.data.resu    lts);
            let data=res.data.results;
            data.forEach(item => {
               if(item.image!=null){
                    item.image=require('../assets/image/'+item.image);
                    item.created_at=Number(item.created_at);
               }
               this.carts.push(item);
            //    console.log(this.carts);
            });
            // console.log(this.carts);
        })
    }
}
</script>

<style scoped>
    .cart{
        background-color:rgb(6,6,6,0.1);
        height: 1000px;
    }
    .cart .goods-item{ 
        margin: 10px 0 10px 0;
    }
    .cart .goods-item .goods-tap{
        padding: 10px 10px 10px 0;
        height: 116px;
        background-color: #fff;
        display: flex
    }
    .cart .goods-item .goods-tap .goods-left{
        margin-right: 13px;
    }
    .cart .goods-item .goods-tap .goods-left .goods-img{
        width: 80px;
        height: 90px;
        margin: 6px 0 0 36px;
        /* border: 1px solid red; */
    }
    .cart .goods-item .goods-tap .goods-left .goods-img img{
        width: 80px;
        height: 90px;
    }
    .cart .goods-item .goods-tap .goods-info .goods-desc{
        /* height: 20px; */
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        display: -webkit-box;
        overflow: hidden;
        text-overflow: ellipsis;
        font-size: 14px;
        font-weight: bold;
    }
    .cart .goods-item .goods-tap .goods-info .goods-add-info{
        /* display: flex; */
        font-size: 12px;
        color: #666;
        margin: 6px 0;
        height: 12px;
    }
    .cart .goods-item .goods-tap .goods-info .goods-add-info .setoff-time{
        float: left;

    }
    .cart .goods-item .goods-tap .goods-info .goods-add-info .setoff-person-num{
        float: right;
    }
    .cart .goods-item .goods-tap .goods-info{
        font-size: 12px;
        color: #666;
    }
    .cart .goods-item .goods-tap .goods-info .goods-price-ico{
        font-size: 10px;
        color: #f60;
    }
    .cart .goods-item .goods-tap .goods-info .goods-price-num{
        font-size: 17px;
        color: #f60;
    }
</style>

