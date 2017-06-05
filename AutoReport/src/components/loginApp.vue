<template>
	<div class="loginApp container content">
		<div class="view row ">
			<img v-bind:src="img" class = 'appicon'  />
		</div>
		<div class="view row ">
			<downloads :isWeixin='isWeixin'></downloads>
		</div>
	</div>
</template>

<script>	
	import downloads from './downLoads'
	
	export default{
		data(){
			return {
				img:require('../assets/default-icon.png')
			}
		},
		components:{
			downloads
			
		},
		props:['isWeixin']
	}
</script>

<style>
	.content {
    	padding-top: 40px;
    	/*padding-bottom: 40px;*/
	}

	.view{
		text-align: center;
	}

	.margin-bottom-30{
		margin-bottom: 30px;
	}

	.appicon{
		width: 120px;
	    height: 120px;
	    -webkit-border-radius: 24px;
	    -moz-border-radius: 24px;
	    border-radius: 24px;
	    border: 1px solid #ddd;
	}
</style>