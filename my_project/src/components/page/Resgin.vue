<template>
    <div class="login-wrap">
        <div class="ms-title">后台管理系统</div>
        <div class="ms-login">
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" class="demo-ruleForm">
                <el-form-item prop="username" label="帐号">
                    <el-input v-model="ruleForm.username" placeholder="请输入帐号"></el-input>
                </el-form-item>
                <el-form-item prop="password" label="密码">
                    <el-input type="password" placeholder="请输入密码" v-model="ruleForm.password" auto-complete="off"  @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>

                <el-form-item prop="checkpass" label="确认密码">
                    <el-input type="password" placeholder="确认密码" v-model="ruleForm.checkpass"  auto-complete="off" @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>

                <el-form-item prop="name" label="姓名">
                    <el-input   v-model="ruleForm.name" placeholder="请输入姓名"  @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>

                <el-form-item prop="sex" label="性别">
                	<el-radio-group v-model="ruleForm.sex" @keyup.enter.native="submitForm('ruleForm')">
					      <el-radio label="男"></el-radio>
					      <el-radio label="女"></el-radio>
					</el-radio-group>
                </el-form-item>                
                
                <el-form-item prop="age" label="年龄">
                    <el-input   v-model="ruleForm.age"  @keyup.enter.native="submitForm('ruleForm')"></el-input>
                </el-form-item>
	
                <div class="login-btn">
                    <el-button type="primary" @click="submitForm('ruleForm')">注册</el-button>
                </div>
                <p style="font-size:13px;line-height:50px;color:#42B983;" v-on:click="onClickMe">* 已有帐号? 点击登录</p>
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
        		  callback()
        		}
        	};        	

			
			var validatecheckpass = (rule,value,callback)=>{
				if (value === '') {
			          callback(new Error('请再次输入密码'));
		        } else if (value !== this.ruleForm.password) {
		          	  callback(new Error('两次输入密码不一致!'));
		        } else {
		          	  callback();
		        }
			}
		
		   var validatename = (rule,value,callback)=>{
				if (value === '') {
			          callback(new Error('请输入姓名'));
		        } else if (value.length>10) {
		          	  callback(new Error('姓名的长度不能大于10!'));
		        } else {
		          	  callback();
		        }		   			   	
		   }
		   
			var validateage = (rule, value, callback) => {
		        if (!value) {
		          return callback(new Error('年龄不能为空'));
		        }else if (!Number.isInteger(value*1)) {
		          return  callback(new Error('请输入数字值'));
		        }else{
		            if(value < 18) {
		              return callback(new Error('必须年满18岁'));
		            }else{
		              callback();
		            }
		        }		        
			}
			
            return {
                ruleForm: {
                    username: '',
                    password: '',
                    checkpass: '',
                    name:'',
                    sex:'',
                    age:'',
                },
                rules: {
                    username: [
                        { validator:validateUsername,trigger: 'blur' }
                    ],
                    password: [
                        { validator:validatePassword,trigger: 'blur' }
                    ],
                    checkpass: [
                        { validator:validatecheckpass,trigger: 'blur' }
                    ],
                    name: [
                        { validator:validatename,trigger: 'blur' }
                    ],
                    age: [
                        { validator:validateage,trigger: 'blur' }
                    ],
                    sex: [
                        { required: true, message: '请选择性别', trigger: 'change' }
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
                        this.onClickMe();
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            onClickMe(){
            	let data= this.ruleForm;
            	this.$emit('onClickfinish',data,false);
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
        top:40%;
        width:100%;
        margin-top: -230px;
        text-align: center;
        font-size:30px;
        color: #fff;

    }
    .ms-login{
        position: absolute;
        left:50%;
        top:38%;
        width:300px;
        height:420px;
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