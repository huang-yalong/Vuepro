<template>

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
</template>
<script>
export default {
    data(){
        return {
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
        },
    },
    mounted(){
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
    /*.discuss .bbt{
        position: fixed;
        bottom: 0px;
        left: 0px;
        width: 100%;
        height: 50px;
        background-color: #fff;
        padding: 8px 2px;
    }
     .discuss .bg{
        position: relative;
        
    }
    .discuss .bbt .btext{
        width: 100%;
        border: 1px solid #333;
        border-radius: 21px;
        padding: 5px 0px 5px 5px;
        font-size:14px;
        background-color: #f5f5f5; 
    }
    .discuss .bg .bbt input{
        position: absolute;
        left: 0px;
        top: 2px;
        width: 100%;
        height: 21px;
        border-radius: 21px;
        opacity: 0;
    }
    .imp{
        width: 100%;
        position: absolute;
        left: 0px;
        background-color: #fff;
        padding: 20px 0px;
        display: none;
    }
    .discuss .imp #tar{
        width: 80%;
        height: 100px;
        vertical-align: bottom;
        outline: none;
    }
    .discuss .imp .send{
        color: rgba(51,51,51,0.6);
        margin-left: 10px;
    }
    .discuss .assist{
        color: #333;
        text-decoration: none;
    } */
</style>
