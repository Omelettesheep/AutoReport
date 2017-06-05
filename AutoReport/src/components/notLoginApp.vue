<template>
	<div class="notLoginApp container content">
		<div class="col-md-6 col-md-offset-3 col-sm-8 col-sm-offset-2">
	            <div class="servive-block servive-block-default">
	                <div class="margin-bottom-30"></div>
	                <div class="margin-bottom-30">
	                    <img v-bind:src="img" class = 'appicon' />
	                </div>
	                <h2 class="heading-md margin-bottom-30">请输入用户名及密码</h2>
	                <p>该应用设置了安装密码<br>请输入用户名密码继续</p>
	                <form method="post" id="form" @submit.prevent="submit">
						<div class="input-group margin-bottom-20">
	                            <span class="input-group-addon"><span class="glyphicon glyphicon-user"></span></span>
	                            <input v-model='user.username' type="text" id="username" class="form-control text-center " name="username" placeholder="请输入用户名">
	                    </div>
	                    <div class="input-group margin-bottom-30">
	                            <span class="input-group-addon"><span class="glyphicon glyphicon-lock"></span></span>
	                            <input v-model='user.password' type="password" id="password" class="form-control text-center " name="password" placeholder="请输入密码">
	                    </div>
	                    <div class="col-lg-12">
	                        <button type="submit" id="submitButton" class ="btn-u btn-u-green"  v-bind:disabled="isPress" >{{message}}</button>
	                        
	                    </div>
	                </form>
	                <div class="margin-bottom-30"></div>
	            </div>
	        </div>
	</div>
</template>

<script>	
	import downloads from './downLoads'
	export default{
		data(){
			return {
				user:{
					username:'yangyi7',
					password:'return1;'
				},
				img:require('../assets/default-icon.png'),
				isPress: false,
				message:"立刻进入"
			}
		},
		components:{
			downloads
		},
		methods:{
			submit:function(){
				var formData = JSON.stringify(this.user);
				this.isPress = "disabled";
				this.message = "请稍等...";
				this.$http.get('/api/login?',{
						params:{
							username:this.user.username,
							password:this.user.password
						}
					}).then((response) => {
					this.isPress = false;
					this.message = "立刻进入";
					if(response.body.code === 810004)
					{
						alert(response.body.msg);
					}
					else{
						this.$emit("listenLoginChange",true)
					}
               		// 
           		}, (response) => {
           			this.isPress = false;
					this.message = "立刻进入";
           			// console.log("No"+response.data);
               		// error callback
           		});
			}
		}
	}
</script>

<style>
	.servive-block-default{
		    background: #fafafa;
    		border: solid 1px #eee;
	}
	.servive-block{
		padding: 20px 30px;
		padding-bottom: 35px;
	    text-align: center;
	    margin-bottom: 20px;
	}
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
	
	.margin-bottom-20{
		margin-bottom: 20px;
	}

	.appicon{
		width: 120px;
	    height: 120px;
	    -webkit-border-radius: 24px;
	    -moz-border-radius: 24px;
	    border-radius: 24px;
	    border: 1px solid #ddd;
	}

	h2.heading-md {
    font-size: 20px;
    line-height: 24px;
	}

	.btn-u.btn-u-green {
    background: #2ecc71;
	}
	.btn-u {
	    background: #1abc9c;
	}
	.btn-u {
	    border: 0;
	    color: #fff;
	    font-size: 14px;
	    cursor: pointer;
	    font-weight: 400;
	    padding: 4px 13px;
	    position: relative;
	    background: #72c02c;
	    display: inline-block;
	    text-decoration: none;
	}

	.servive-block-default:hover {
    box-shadow: 0 0 8px #eee;
	}

	.btn-u.btn-u-green:hover, .btn-u.btn-u-green:focus, .btn-u.btn-u-green:active, .btn-u.btn-u-green.active{
	background: #27ae60;
	}

	.grey{
		background: grey;
	}

</style>