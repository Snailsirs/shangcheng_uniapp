<template>
	<view>
		<!-- 第一部分 -->
		<view class="u-f u-f-jsb content1">
			<view class="u-f-ac" style="width: 70%;">
				<view>
					<image class="user-logo" src="../../static/demo/userpic/10.jpg" mode="widthFix"></image>
				</view>
				<view style="margin-left: 20upx;">
					<view class="user-name">
						<text>理想</text>
						<view class="cu-tag sm bg-yellow radius">白金会员</view>
					</view>
					<view style="margin-top: 25upx;">
						<view class="cu-tag round sm line-blue" style="line-height: 32upx;">172****1234</view>
						<view class="cu-tag round sm line-blue" style="line-height: 32upx;">认证会员</view>
					</view>
				</view>

			</view>
			<view class=" flex align-center">
				<button class="cu-btn line-red">
					<text class="cuIcon-redpacket_fill text-red"></text>
					拼单返现</button>
			</view>
		</view>
		<view class="yueka-fa u-f-ajc">
			<view class="yueka u-f-ac u-f-jsb">
				<view class="u-f-ac">
					<text style="font-size: 120%;">省钱月卡</text>
					<text style="margin-left: 10upx;margin-right: 10upx;">|</text>
					<text>帮你省钱1100</text>
				</view>
				<view class="u-f-ac">
					<button class="cu-btn round sm bg-red">领取通用券</button>
					<view class="cuIcon-right"></view>
				</view>
			</view>
		</view>
		<view style="margin-top: 5upx;" class="u-f-ajc u-f-column">
			<view class="u-f-ac u-f-column  bg-white" style="width: 700upx;height: 220upx;border-radius: 20upx;">
				<view style="width: 90%;" class="u-f u-f-jsb">
					<text style="font-size: 120%;">我的订单</text>
					<text class="txte-gray">查看全部</text>
				</view>
				<view class="u-f-ac u-f-jsa" style="width: 90%;">
					<view style="position: relative;" class="u-f-ac u-f-column" v-for="(item,index) in orders" :key="index">
						<view :class="item.icon" style="font-size: 60upx;color: gray;"></view>
						<view v-if="item.num!=0" style="position: absolute;top: 0;right: 0;" class="cu-tag bg-red round sm">{{item.num}}</view>
						<view>
							{{item.text}}
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="list-content">
			<view 
			@tap="gopage(index)"
			class="bg-white list-item u-f-ac" 
			v-for="(item,index) in lists" :key="index">
				<text style="font-size: 130%;margin-right: 10upx;" :class="item.icon"></text><text>{{item.text}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				orders: [{
						text: "代付款",
						icon: "cuIcon-pay",
						num: 0,
						id: 1,
					},
					{
						text: "代分享",
						icon: "cuIcon-share",
						num: 5,
						id: 2,
					},
					{
						text: "代发货",
						icon: "cuIcon-time",
						num: 0,
						id: 3,
					},
					{
						text: "代收货",
						icon: "cuIcon-deliver",
						num: 10,
						id: 4,
					},
					{
						text: "代评价",
						icon: "cuIcon-comment",
						num: 5,
						id: 5,
					},
				],
				lists:[
					{
						text:"我的收藏",
						icon:"cuIcon-favorfill text-orange"
					},
					{
						text:"退款售后",
						icon:"cuIcon-refund text-black"
					},
					{
						text:"收货地址",
						icon:"cuIcon-location text-brown"
					},
					{
						text:"官方客服",
						icon:"cuIcon-phone text-blue"
					},
					{
						text:"系统设置",
						icon:"cuIcon-settingsfill text-cyan"
					},
					{
						text:"注销登录",
						icon:"cuIcon-roundclosefill text-red",
						url:"../login/login"
					}
				]
			}
		},
		methods: {
			gopage(item){
				// console.log(item);
				var url=this.lists[item].url;
				if(url!=null&&url!=undefined){
					uni.reLaunch({
						url:url
					})
				}
				
			}
		}
	}
</script>

<style scoped>
	.list-content{
		margin-top: 20upx;
	}
	.list-item{
		height:80upx;
		padding: 0 20upx 0 40upx;
		border-bottom: 1upx solid #ddd;
	}
	uni-view {
		line-height: 1.5;
	}

	.user-logo {
		width: 150upx;
		height: 120upx;
	}

	.content1 {
		padding: 30upx;
		background-color: #F8F8F8;
	}

	.user-name {
		font-size: 130%;
	}

	.yueka-fa {
		background-color: #F8F8F8;
	}

	.yueka {
		width: 600upx;
		height: 80upx;
		background-color: #FADBD9;
		border-top-left-radius: 18upx;
		border-top-right-radius: 18upx;
		color: rgb(187, 50, 52);
		padding: 0 20upx;
		font-weight: 550;
	}
</style>
