<template>
	<div class="wrapper">
		<transition name="el-zoom-in-center">
	    	<div class="wrapper" v-show="oshow">
				<v-resgin @onClickfinish = "onClickfinish"></v-resgin>
			</div>
        </transition>	    	  
        
	    <transition name="el-zoom-in-center">
	    	<div class="wrapper" v-show="!oshow">
				<v-login @onClickfinish = "onClickfinish"></v-login>	
			</div>
        </transition>	    	  
	</div>	 
</template>
<script>
    import vLogin from './Login.vue';
    import vResgin from './Resgin.vue';
    export default {   
        components:{
            vLogin, vResgin
        },
        data() {
            return {
            	oshow:true
            }
        },
        methods: {
        	onClickfinish(...data){
        		this.oshow=data[1];
        	}        
        }
    }
</script>

<style scoped>
   .transition-box {
			    margin-bottom: 10px;
			    width: 200px;
			    height: 100px;
			    border-radius: 4px;
			    background-color: #20A0FF;
			    text-align: center;
			    color: #fff;
			    padding: 40px 20px;
			    box-sizing: border-box;
			    margin-right: 20px;
	 }
</style>