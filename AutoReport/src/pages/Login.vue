<template>
	<div container>
		<common-header></common-header>
		<tips v-if='isLogin && isWeixin'></tips>
		<loginApp v-if="isLogin" :isWeixin='isWeixin'></loginApp>
		<notLoginApp v-else  @listenLoginChange='changeLogin'></notLoginApp>
		<hr class="devider devider-dotted">
		<qr :isLogin='isLogin'></qr>
		<history v-if="isLogin"></history>
	</div>
</template>

<script>
	import commonHeader from '../components/commonHeader'
	import loginApp from '../components/loginApp'
	import qr from '../components/qr'
	import notLoginApp from '../components/notLoginApp'
	import history from '../components/history'
	import tips from '../components/tips'
	export default{
		data(){
			return{
				isLogin:false,
				isWeixin:true
			}
		},
		components:{
			commonHeader,
			loginApp,
			qr,
			notLoginApp,
			history,
			tips
		},
		methods:{
			changeLogin:function(data){
				this.isLogin = data;
			}
		},
		created:function(){
			var ua = navigator.userAgent.toLowerCase();
			if(ua.match(/MicroMessenger/i)=="micromessenger") {
				this.isWeixin =  true;
			} else {
				this.isWeixin =  false;
			}
		}
	}
</script>

<style>
	.margin-bottom-20{
		margin-bottom: 20px;
	}

	.devider-dotted{
		border-top: 2px dotted #eee;
	}

	hr{
		margin:30px 0;
	}
</style>
