<template>
    <div>
            <mt-header title="注册">
                <router-link to="/me" slot="left">
                    <mt-button icon="back"></mt-button>
                </router-link>
            </mt-header>
        <div>
            <mt-field type="text" label="用户名" placeholder="请输入用户名" disabledClear :state="username" v-model="uname" @blur.native.capture="checkuname">
            </mt-field>
             <mt-field type="password" label="密码" placeholder="请输入密码" disabledClear :state="password" v-model="upwd" @blur.native.capture="checkupwd">
            </mt-field>
             <mt-field type="password" label="确认密码" placeholder="请再次输入密码" disabledClear :state="cpassword" v-model="cpwd" @blur.native.capture="checkcpwd">
            </mt-field>
            <mt-button type="danger" size="large" class="btn1" @click="reg()">注册</mt-button>
            <h5 align="center">注册即同意<a href="#">用户服务协议</a>和<a href="#">隐私政策</a></h5>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            uname:"",
            upwd:"",
            cpwd:"",
            username:"",
            password:"",
            cpassword:""
        }
    },
    methods:{
        checkuname(){
            let uname=this.uname;
            let unameRegExp=/^[0-9A-Za-z_]{6,12}$/;
            if(unameRegExp.test(uname)){
                this.username="success";
                return true;
            }else{
                this.username="error";
                this.$toast({
                    message:'请输入合法用户名',
                    postion:'middlue',
                    duartion:2000
                });
                return false;
            }
        },
        checkupwd(){
            let upwd=this.upwd;
            let upwdRegExp=/^[0-9A-Za-z_]{6,10}$/;
            if(upwdRegExp.test(upwd)){
                this.password="success";
                return true;
            }else{
                this.password="error";
                this.$toast({
                    message:'请输入合法密码',
                    postion:'middlue',
                    duartion:2000
                });
                return false;
            }
        },
        checkcpwd(){
            let cpwd=this.cpwd;
            if(cpwd==this.upwd && cpwd!==''){
                this.cpassword="success";
                return true;
            }else{
                this.cpassword="error";
                this.$toast({
                    message:'两次密码不一致',
                    postion:'middlue',
                    duartion:2000
                });
                return false;
            }
        },
        reg(){
            if(this.checkuname() && this.checkupwd() && this.checkcpwd()){
                this.axios.post('/register','uname='+this.uname+'&upwd='+this.upwd).then(res=>{
                    if(res.data.code==0){
                        this.$messagebox('注册提示','对不起，用户已存在');
                    }else{
                        this.$messagebox('注册提示','注册成功');
                        this.$router.push('/login');
                    }
                })
            }
        }
    }

}
</script>
<style>
    .mint-header{
        background-color:#00A99D !important;
        margin-bottom: 10px;
    }
    .btn1{
        margin-top: 10px;
    }
</style>