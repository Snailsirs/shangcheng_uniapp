<template>
	<view>
		<view style="height: 150upx;"></view>
		<view class="u-f-ac u-f-column">
			<image class="logo" src="../../static/demo/userpic/3.jpg" mode=""></image>
			<view style="margin-top: 30upx;color: gray;">正品低价有保障！！！</view>

		</view>
		<view>
			<view class="input-fa">
				<input class="log-input" v-model="form.phone" placeholder="用户名/邮箱/手机号" />
			</view>
			<view class="input-fa u-f-ac">
				<input class="log-input" :password="true" :placeholder="status==0?'请输入密码':'请输入验证码'" v-model="form.password" />
				<button :disabled="yzmclick" @tap="huoquyzm" v-if="status==1" class="cu-btn bg-gradual-orange">{{yzmtext}}</button>
			</view>
			<view class="u-f u-f-jsb input-fa" style="margin-top: 15upx;">
				<text>忘记密码？</text>
				<text>新用户注册</text>
			</view>
		</view>
		<view style="width: 50%; margin: 30upx auto;">
			<button @tap="login" class="bg-gradual-red round">登录</button>
		</view>
		<view class="u-f-ac u-f-jsb" style="margin-top: 30upx;">
			<view class="line"></view>
			<view style="color: gray;">其它登录方式</view>
			<view class="line"></view>
		</view>
		<view class="u-f-ac u-f-jsa" style="margin-top: 40upx;">
			<view class="u-f-ac u-f-column" style="width: 20%;">
				<image class="wx" src="../../static/zcimg/weixin.png"></image>
				<view style="margin-top: 10upx;">微信登录</view>
			</view>
			<view @tap="changestatus" class="u-f-ac u-f-column" style="width: 20%;">
				<image class="wx" :src="status==0?'../../static/zcimg/phone.png':'../../static/zcimg/mima.png'"></image>
				<view style="margin-top: 10upx;">{{status==0?'验证码':'密码'}}登录</view>
			</view>
		</view>
		<view style="position: fixed;bottom: 10upx;color: gray;text-align: center;width: 100%;">
			登录代表您已同意！<text class="text-blue">【隐私政策】</text>
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				yzmtext:"获取验证码",
				yzmclick:false,
				status: 0, //0密码登录  1验证码登录
				form: {
					phone: "",
					password: ""
				}
			}
		},
		methods: {
			huoquyzm(){
				var its=this;
				if(this.form.phone.length!=11){
					uni.showToast({
						icon:"none",
						title: '请输入正确手机号格式'
					});
				}
				if(this.yzmtext=="获取验证码"){
					this.yzmclick=true;
				}else{
					return;
				}
				var seconds=60;
				var jishiqi = setInterval(()=>{
					seconds--;
					its.yzmtext=seconds+"秒后重发";
					if(seconds<=0){
						its.yzmtext="获取验证码";
						its.yzmclick=false;
						clearInterval(jishiqi);
					}
				},1000);
			},
			changestatus() {
				this.status = this.status == 0 ? 1 : 0;
			},
			login() {
				uni.request({
					url: "http://192.168.31.179:4444/user/login",
					data: {
						phone: this.form.phone,
						password: this.form.password
					},
					method: "POST",
					success: (res) => {
						uni.showToast({
							icon:"none",
							title:res.data.desc
						});
						console.log(res.data);
						if (res.data.status==0) {
							uni.setStorageSync("uid",res.data.uid);
							var b = uni.getStorageSync("uid")
							uni.switchTab({
								url:"../my/my"
							})
						}
					}
				})
			}
		}
	}
</script>

<style>
	.wx {
		width: 80upx;
		height: 80upx;
	}

	.line {
		height: 1upx;
		background-color: #DDDDDD;
		flex-grow: 1;
	}

	.logo {
		width: 200upx;
		height: 200upx;
	}

	.log-input {
		height: 100upx;
		border-bottom: 1upx solid #DDDDDD;
		flex-grow: 1;
	}

	.input-fa {
		padding: 0 40upx;
	}
</style>
