<template>
    <div class="login-wrap">
        <div class="ms-title">后台管理系统</div>
        <div class="ms-login">
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="0px" class="demo-ruleForm">
                <el-form-item prop="username">
                    <el-input v-model="ruleForm.username" placeholder="username"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input type="password" placeholder="password" v-model="ruleForm.password" @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>
                <div class="login-btn">
                    <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
                </div>
                <p style="font-size:13px;line-height:50px;color:#42B983;"  v-on:click="onClickMe">* 还未注册? 点击注册</p>
            </el-form>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
        	var validateUsername = (rule,value,callback)=>{
	        	var b=/^1[34578]\d{9}$/g;        			        	
        		var falg=b.test(value);
        		if(!value){
        			return callback(new Error('帐号不能为空!'));
        		}else if(!falg){
        			return callback(new Error('帐号只能手机号码!'));
        		}else if(value.length<5){
        			return callback(new Error('长度不能小于5!'));
        		}else{
        			return callback()
        		}
        	};
							        	
        	var validatePassword = (rule,value,callback)=>{ 
        		var b = /^[0-9a-zA-Z]*$/g;
        		var falg = b.test(value);
        		if(!value){
        			return callback(new Error('密码不能为空!'));
        		}else if(value.length>11){
        			return callback(new Error('密码的长度不能大于11位!'));
        		}else if(!falg){
        			return callback(new Error('密码只能是数字、字母或数字和字母的组合!'));
        		}else{
        			return callback()
        		}
        	};        	
        	        		
            return {
                ruleForm: {
                    username: '',
                    password: '',
                    checkpass:'',
                },
                rules: {
                    username: [
                        { validator:validateUsername,trigger: 'blur' }
                    ],
                    password: [
                        { validator:validatePassword,trigger: 'blur' }
                    ]
                }
            }
        },
        methods: {
            submitForm(formName) {
                const self = this;
                self.$refs[formName].validate((valid) => {
                    if (valid){
                        localStorage.setItem('ms_username',self.ruleForm.username);
                        self.$router.push('/readme');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            onClickMe(){
            	let data= this.ruleForm;
            	this.$emit('onClickfinish',data,true);
            }
        }
    }
</script>

<style scoped>
    .login-wrap{
        position: relative;
        width:100%;
        height:100%;
    }
    .ms-title{
        position: absolute;
        top:50%;
        width:100%;
        margin-top: -230px;
        text-align: center;
        font-size:30px;
        color: #fff;

    }
    .ms-login{
        position: absolute;
        left:50%;
        top:50%;
        width:300px;
        height:160px;
        margin:-150px 0 0 -190px;
        padding:40px;
        border-radius: 5px;
        background: #fff;
    }
    .login-btn{
        text-align: center;
    }
    .login-btn button{
        width:100%;
        height:36px;
    }
</style>