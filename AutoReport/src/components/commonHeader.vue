<template>
	<div class="head row-fluid breadcrumbs margin-bottom-20">
	    <div class="container">
	        <h1 class="pull-left">AutoReport</h1>
	        <ul class="pull-right breadcrumb">
	            <li>版本：{{versions.version}}</li>    
	            <li>大小：{{versions.size}}</li>
	            <li>{{versions.time}}</li>
	        </ul>
	    </div><!--/container-->
	</div>
</template>

<script>
	export default{
		data(){
			return{
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
	.head{
		border-top: 2px solid #eee;
	}

	.breadcrumbs{
		overflow: hidden;
		padding: 10px 0 6px;
		border-bottom: solid 1px #eee;
		border-top: 2px solid #eee;
		background: url(../assets/breadcrumbs.png) repeat;
	}

	.breadcrumb{
		top: 10px;
		padding-right: 0;
		background: none;
		position: relative;
	}

	.breadcrumbs h1{
		color: #666;
		font-size: 22px;
		line-height: 35px;
		margin-top: 8px;
	}

	.margin-bottom-20{
		margin-bottom: 20px;
	}

	@media (max-width: 550px){
		.breadcrumbs h1.pull-left {
		    margin-bottom: 0;
		}
	}
		
	@media (max-width: 550px)
	{
		.breadcrumbs h1.pull-left, .breadcrumbs ul.pull-right {
    	width: 100%;
    	text-align: center;
		}
	}

</style>

