<template>
	<div class="updateInfo">
	    <div class="col-md-8 col-md-offset-2" style="word-break:break-all;">
	        <div class="tag-box tag-box-v6 margin-bottom-30">
	            <h2>更新说明</h2>
	            {{versions.time}}         
	        </div>
	    </div>
	</div>
</template>
<script>
	export default{
		data(){
			return {
				versions:{}
			}
		},
		created:function(){
			this.$http.get('/api/info').then((data)=>{
				this.versions = data.body.result;
			})
		}
	}
</script>
<style>
	.margin-bottom-30{
		margin-bottom: 30px;
	}

	.tag-box-v6{
		background: #fafafa;
    	border: solid 1px #eee;
	}
	
	.tag-box{
		padding: 20px;
	}

</style>