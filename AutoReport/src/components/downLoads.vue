<template>
	<div class="downloads margin-top-30">
		<div class="span12 margin-bottom-20" >
			<div id="showtext" v-bind:class="{ display_none: !isShown }">正在安装，请按 Home 键在桌面查看</div>
			<div class="loading" v-bind:class="{ display_none:!isLoading,display_lb:isLoading }"></div> 
			<a href="javascript:void(0);" class="btn-u btn-t-lg"  v-bind:class="{ display_none: isIOS }" v-on:click="downLoad" >
				<span class="glyphicon glyphicon-download-alt" aria-hidden="true"> </span> 
				点击安装
			</a>
		</div>
		<div class="span12">
			<span class="label label-info">适用于IOS设备</span>
			<span class="label label-danger">企业版</span>
		</div>
	</div>
</template>
<script>
	export default{
		data(){
			return{
				isLoading:false,
				isIOS:false,
				isShown:false,
			}
		},

		props:['isWeixin'],

		methods:{
			downLoad:function(){
				if(!this.checkUserAgent()) {
					if(!this.isWeixin){
						this.isIOS = true;
					 	this.isLoading = true;
					 	var that = this;
						var time = setInterval(function(){
						 	that.isLoading = false;
						 	that.isShown = true;
						 	clearInterval(time)
						 	
						 },5000)
					} 
					else{
						console.log(this.isWeixin);
						alert("请点击微信右上角按钮，然后在弹出的菜单中，点击在浏览器中打开，即可安装");
					}
				}
				

			},
			checkUserAgent:function(){
				var userAgentInfo = navigator.userAgent;
		        var Agents = ["Android", "iPhone","SymbianOS", "Windows Phone", "iPod"];
		        var flag = true;
		        for (var v = 0; v < Agents.length; v++) {
		            if (userAgentInfo.indexOf(Agents[v]) > 0) {
		            	var env = Agents[v];
		                flag = false;//is not PC
		                break;
		            }
		        }
		        //is the PC
		        if(flag){
		        	alert("请在手机上使用浏览器打开本页面，或者扫描下面的二维码，即可安装");
		        	return flag;//not in condition
		        }
		        //not the PC
		        else{
		        	if(env != 'iPhone'){
		        		alert("您的手机不是苹果系统，无法安装IOS应用");
		        		return true;//not in condition
		        	}
		        	else{
		        		//this is the iphone
		        		return false;
		        	}
		        }

			}
		}
	}
</script>

<style>
	.span12{
		text-align: center;
	}

	.margin-top-30{
		margin-top: 30px;
	}

	span.label {
	    font-size: 12px;
	    font-weight: 400;
	    padding: 3px 7px;
	}

	.btn-u{

		background: #1abc9c;
		border: 0;
	    color: #fff;
	    cursor: pointer;
	    font-weight: 400;
	    position: relative;
	    display: inline-block;
	    text-decoration: none;
	    font-size: 18px;
   		padding: 10px 25px;
	}
	
	a, a:focus, a:hover, a:active {
	    outline: 0 !important;
	    background: #28caad;
	    text-decoration: none;
	    color:#fff;

	}
	#showtext{
		text-align: center;
	    color: #1abc9c;
	    font-size: 14px;
	}

	.loading{
	    background-color: transparent;
	    width: 45px;
	    height: 45px;
	    border: 1px solid #1abc9c;
	    border-radius: 50%;
	    border-top-color: transparent;
	    border-left-color: transparent;
	    -webkit-transition: all .25s;
	    transition: all .25s;
	    -webkit-animation: rotate .6s linear infinite;
	    animation: rotate .6s linear infinite;
	}
	
	.display_none{
		display: none;
	}

	.display_lb{
		display: inline-block;
	}

	@keyframes rotate{
		0% {
    	-webkit-transform: rotate(0);
    	transform: rotate(0);
		}
		100% {
   		 -webkit-transform: rotate(360deg);
    	transform: rotate(360deg);
		}
	}
   
</style>