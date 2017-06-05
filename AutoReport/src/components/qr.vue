<template>
	<div class="qr container">
		<div class="span12 margin-bottom-30">
			请用手机扫描下面的二维码安装<br><br>
			<!-- <img v-bind:src="img" width="156px" height="156px"> -->
			<div>
				<div id='code'></div>
				<canvas id="canvas"></canvas>
			</div>
		</div>
		<div class="row margin-bottom-40" v-if='isLogin'>
			<updateInfo></updateInfo>
		</div>
		<hr class="devider devider-dotted" v-if='isLogin'>
		<!-- <vue-q-art :config="config" :downloadButton="downloadButton"></vue-q-art> -->
		
	</div>
</template>

<script>
import updateInfo from './updateInfo'
import Vue from 'vue'
import QRCode from 'qrcode'
Vue.use(QRCode)


	export default{
		data(){
			return {
				img:require('../assets/JcZe.png'),
		        codes:''
			}
		},
		components:{
			updateInfo
		},
		props:['isLogin'],
		methods:{
			useqrcode(){

				var url = window.location.href;
				console.log(url);
				var canvas = document.getElementById('canvas')
				QRCode.toCanvas(canvas, url, function (error) {
				if (error) console.error(error)
				})
			}
		},
		mounted(){
			this.useqrcode();
		}
	}
	
</script>

<style>
	.span12{
		text-align: center;
	}

	.margin-bottom-30{
		margin-bottom: 30px;
	}

	.margin-bottom-40{
		margin-bottom: 40px;
	}

	.tag-box h2 {
		margin-top: 5px;
	    font-size: 20px;
	    line-height: 25px;
	}

	#canvas{
		margin-top: -18px;
		width:200px!important;
		height:200px!important;
	}

</style>