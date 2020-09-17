<template>
 <div id="dateContainer">
    <!-- <div class="date__showNowTime">
        今天是 <span v-text="ynow"></span>年<span v-text="mnow+1"></span>月<span v-text="dnow"></span>日
   </div> -->
   <div class="nowTime">
        <!-- <button class="preMon" @click="preMon">上个月</button> -->
        <div class="preMon" @click="preMon"></div>
        <div class="thisMon">
            <span v-text="ynow"></span>/
             <!-- <span v-text="mnow+1"></span> -->
             <span v-text="mnow<9 ? '0'+(mnow+1) : mnow+1"></span>
        </div>
        <!-- <button class="nextMon" @click="nextMon">下个月</button> -->
        <div class="nextMon" @click="nextMon"></div>
   </div>
   <table id="table" @click="hendl($event)">
       
   </table>
   <div class="bm-form">
       <div class="m-form">
           <div class="title">
               请选择出行人数
           </div>
           <div class="item">
               <div class="tit">成人</div>
               <div class="m-number">
                   <span class="minus react-cursor">
                       -
                   </span>
                   
                   <div class="input">
                       <!-- <span>2</span> -->
                       2
                   </div>
                   <span class="plus react-cursor">
                       +
                   </span>
               </div>
               <div class="tit ml15">
                   <p>儿童</p>
               </div>
               <div class="m-number">
                   <span class="minus react-cursor">
                       -
                   </span>
                   <div class="input">
                       <span class="inp">0</span>
                   </div>
                   <span class="plus react-cursor">
                       +
                   </span>
               </div>
           </div>
        </div>
        <div class="m-step" @click="sure">
            <div class="text">确定</div>
        </div>
   </div>
</div>
</template>
<script>
export default {
  data() {
   return {
    t_str:'',
    newDate: '',//当前的日期的信息
    ynow: '',//当前的年数
    mnow: '',//当前的月份
    dnow: '',//当前的天数
    firstDay: '',//第一天
    firstnow: '',//当前的星期
    m_days: [],//每个月的天数
    tr_str: '',//行数
    dayVal:""//日期值
   }
  },
  methods: {
   getDaysInfo() {
    var _this = this;
    this.sureDate(_this);
   },
   is_leap(year) {//判断是不是闰年
    return (year%100==0?(year%400==0?1:0):(year%4==0?1:0));
   },
   //下面的是画表格的方法，这个方法会根据数据画出我们需要的表格
   drawTable(jsonHtml) {
    var _this = this;
    var str = `
    <tr class="xiqi">
     <td class="isRed">日</td>
     <td>一</td>
     <td>二</td>
     <td>三</td>
     <td>四</td>
     <td>五</td>
     <td class="isRed">六</td>
    </tr>`;
    var idx = '',date_str = '',isRed = '',hasMsg='',isgray='';
    var day_now=new Date().getMonth();
    // console.log(this.mnow);
    // console.log(day_now);
    // 多少行
    for(var i = 0; i< _this.tr_str; i++) {
     str+='<tr>';
    //  多少列
     for(var k = 0; k < 7; k++) {
        // 每页td的个数
       idx = i*7+k;
    //    console.log(idx);
    //周六,日标红
       isRed = (k===0||k===6)?"isRed":"";
    //    console.log(date_str);
    //     console.log(this.dnow);
    //    console.log(date_str<this.dnow);
    //    console.log(this.mnow<=day_now);
    //    console.log(isRed);
    // console.log(_this.firstnow);
    //所有td对应的日期,但是这时有正有负(第一个td对应的日期为-1,然后是0,1,2,3...)
       date_str=idx-_this.firstnow+1;//(0,7,14,21,28)
    //    console.log(date_str);
      (date_str<=0 || date_str>this.m_days[this.mnow]) ? date_str=" " : date_str=idx-_this.firstnow+1;
    //   date_str==_this.dnow?hasMsg='<td class="thisDay" date="'+date_str +'"><span class="'+isRed +'">'+date_str+'</span></td>':hasMsg='<td date="'+date_str +'"><span class="'+isRed +'">'+date_str+'</span></td>';
        // console.log(date_str);
        // console.log(date_str);
        // console.log(this.dnow);
        isgray = (date_str<this.dnow&&date_str!=" "&&this.mnow-1<day_now||this.mnow<day_now) ? "isgray":"";
        if(date_str<this.dnow&&this.mnow<day_now&&date_str!=" "){   
            date_str==_this.dnow&&this.mnow==day_now?hasMsg='<td class="thisDay" date="'+date_str +'"><span class="'+isRed +'">'+date_str+'</span></td>':hasMsg='<td date="'+date_str +'" class="'+isgray+'" ><span class="'+isRed +'">'+date_str+'</span></td>';
        }else{
         date_str==_this.dnow&&this.mnow==day_now?hasMsg='<td class="thisDay" date="'+date_str +'"><span class="'+isRed +'">'+date_str+'</span></td>':hasMsg='<td date="'+date_str +'" class="'+isgray+'" ><span class="'+isRed +'">'+date_str+'</span></td>';
        }


    //   for(var l = 0, len = jsonHtml.length; l < len; l++) {
    //   if(date_str== jsonHtml[l].date) {
    //    var newStr = '<p>'+jsonHtml[l].msg +'</p>';
    //    date_str==_this.dnow?hasMsg='<td class="thisDay" date="'+date_str +'" class="'+isgray+'"><span class="'+isRed +'">'+date_str+'</span>'+ newStr+'</td>':hasMsg='<td class="'+isgray+'" date="'+date_str +'"><span class="'+isRed +'">'+date_str+'</span>'+ newStr+'</td>';
  
    //   }
    //   }
      str+=hasMsg;
      }
     str+='</tr>';
    }
    var table = document.getElementById('table');
    table.innerHTML = str;
   },
   hendl(event){
        // let tag=$(event.target);
        // if(!(tag.attr("date"))&&!(tag.parent().hasClass("isgray"))){
        //     $('td').removeClass("isblue");
        //     tag.parent().addClass("isblue");
        //     this.dayVal=tag.html();
        // }else{
        //     this.dayVal='';
        // }
        // console.log($("td").not(tag.parent()));
        let tag=event.target;
        // console.log(tag);
        // console.log(tag.hasAttribute("date"));
        //console.log(tag.parentNode.className=="isgray");
         if(!(tag.hasAttribute('date'))&&tag.parentNode.className!="isgray"){
            //  let td=document.getElementsByTagName("td");
            let td=document.querySelectorAll("td:not([class='isgray'])");
            //  console.log(tds);
            for(var i=0;i<td.length;i++){
                    td[i].className="";
            }
             tag.parentNode.className="isblue";
             this.dayVal=tag.innerHTML;
         }else{
             this.dayVal='';
         }
   },
   //两个参数代表的含义分别是this对象以及判断当前的操作是不是在进行月份的修改
   sureDate(_this,other) {
    this.newDate = new Date();//当前日期的信息
    // console.log(this.newDate);
    // console.log(this.newDate);
    this.ynow = this.newDate.getFullYear();//当前的年数
    // console.log(other);
    if(!other) {
        // console.log(other);
     this.mnow=this.newDate.getMonth(); //当前的月份
    }
    this.dnow=this.newDate.getDate(); //今日日期
    this.firstDay = new Date(this.ynow,this.mnow,1);//本年本月的第一天
    // console.log(this.firstDay);
    this.firstnow=this.firstDay.getDay();//当前月第一天星期几
    this.m_days = [31,28+this.is_leap(this.ynow),31,30,31,30,31,31,30,31,30,31];//每个月的天数
    this.tr_str = Math.ceil((_this.m_days[this.mnow] + this.firstnow)/7);//行数
    if(this.mnow<=11&&this.mnow>0){
        this.showMsg();
    }else{
        this.mnow<=0 ? this.mnow=0:this.mnow=11;
        return;
    }
   },
   preMon() {
    var _this = this;
    this.mnow--;
    this.sureDate(_this,"up");
    // console.log(this.mnow);
   },
   nextMon() {
    var _this = this;
    this.mnow++;
    this.sureDate(_this,"next");
    // console.log(this.mnow);
   },
   //通过接口返回的是我们当前的月份对应在日历中需要处理的事项
   showMsg() {
    var jsonHtml = [{
     date: 2,
     msg: ''
    },
    {
     date: 3,
     msg: ''
    },
    {
     date: 4,
     msg: ''
    },
    {
     date: 6,
     msg: ''
    },
    {
     date: 12,
     msg: ''
    },
    {
     date: 15,
     msg: ''
    },
    {
     date: 20,
     msg: ''
    }];
    this.drawTable(jsonHtml)
    // console.log(this);
   },
   sure(){
       let adult=document.getElementsByClassName("input")[0];
       let children=document.getElementsByClassName("inp")[0];
       adult=Number(adult.innerHTML);
    //    console.log(adult);
       children=Number(children.innerHTML);
    //    console.log(children);
       let uid=sessionStorage.getItem("userId");
    //    console.log(uid);
       let date=`${this.ynow}年${this.mnow+1}月${this.dayVal}日`;
       let pid=this.active=this.$route.params.id;
    //    console.log(date);
       if(this.dayVal){
        //    alert("日期不能为空");
        this.axios.post('/lianxi','adult='+adult+'&children='+children+'&uid='+uid+'&date='+date+'&pid='+pid).then(res=>{
            console.log(res.data.message);
        });
        console.log("111");
       }
        
   }
  },
  mounted() {
   //画出当前的月份的天数对应的表格
   this.getDaysInfo();
   //进行数据的获取，显示到对应的位置
  }
}
  </script>
<style scoped>
    #dateContainer{
        margin: 10px;
    }
    #dateContainer .nowTime{
        display: flex;
        justify-content: space-between;
        height: 30px;
    }
    #dateContainer .preMon{
        width: 20px;
        height: 20px;
        background-image: url('../assets/left.png');
    }
    #dateContainer .nextMon{
        width: 20px;
        height: 20px;
        background-image: url('../assets/right.png');
    }
    #dateContainer table{
        width: 100%;
        
    }
    #dateContainer .bm-form{
        width: 100%;
        height: 133px;
        background-color:#f5f5f5;
        position: fixed; 
        top: 77%;
        left: 0px;
    }
    #dateContainer .m-form{
        margin: 10px 0 15px;
        padding: 0 10px 0 15px;
        background-color: #fff;
    }
    #dateContainer .m-form .title{
        font-size: 14px;
        line-height: 35px;
        color: #333;
    }
    #dateContainer .item{
        display: flex;
        margin-right: -10px;
        padding: 10px 10px 10px 0;
        height: 50px;
        line-height: 50px;
        box-sizing: border-box;
        /* border: 1px solid red; */
        vertical-align: middle;
    }
    #dateContainer .tit{
        vertical-align: middle;
        line-height: 28px;
        font-size: 14px;
        color: #333;
    }

    #dateContainer .m-number{
        border: 1px solid #c2f3fa;
        display: flex;
    }
    #dateContainer .m-number .minus{
        width: 33px;
        font-size: 20px;
        display: block;
        line-height: 28px;
        text-align: center;
        cursor: pointer;
        color: #00bcd4;
        border-right:1px solid #c2f3fa; 
    }
    #dateContainer .m-number .input{
        display: block;
        color: #212121;
        font-size: 16px;
        line-height: 30px;
        width: 45px;
        text-align: center;
    }
    #dateContainer .m-number .plus{
        width: 33px;
        font-size: 20px;
        display: block;
        line-height: 28px;
        text-align: center;
        cursor: pointer;
        color: #00bcd4;
        border-left:1px solid #c2f3fa; 
    }
    #dateContainer .ml15{
        margin-left: 15px;
        line-height: 3px;
    }
    #dateContainer .m-step{
        width: 100%;
        height: 48px;
        color: #fff;
        font-size: 17px;
        background-color: #f60;
    }
    #dateContainer .text{
        height: 100%;
        line-height: 48px;
        text-align: center;
    }
</style>
<style>
    #dateContainer table td{
        text-align: center;
        font-size:14px;
        height:49px;
        border-radius: 50%;
        /* background:red; */
        line-height:49px;
    }
    #dateContainer table .xiqi td{
        font-size:16px;
        color:gray;
        width:49px;
        height:49px;
        border-radius: 50%;
        line-height:49px;
    }
    #dateContainer .isblue{
        background-color:#6fb1e2;
        color:#fff;
    }
    #dateContainer td.thisDay{
        background-color:#eee;
    }
   #dateContainer .isgray{
         background-color:green !important; 
        color:rgba(51,51,51,0.3) !important;
        background-color:#f8f8f8 !important;
    }
   
</style>

  