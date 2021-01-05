<template>
	<view>
		<!-- 搜索框 -->
		<view class="cu-bar search bg-gradual-orange">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input v-model="search" placeholder="请输入你想要的商品"></input>
			</view>
			<view class="action">
				<text class="cuIcon-scan" style="font-size: 150%;"></text>
			</view>
		</view>
		<!-- tab -->
		<view>
			<scroll-view scroll-x class="bg-white nav">
				<view class="flex text-center">
					<view class="cu-item flex-sub" :class="index==tabIndex?'text-orange cur':''" v-for="(item,index) in TabList" :key="index"
					 @tap="qiehuan(index)" :data-id="index">
						{{item}}
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 轮播 -->
		<swiper style="margin-top: 10upx;" class="square-dot" :indicator-dots="true" :circular="true">
			<swiper-item>
				<image class="swiperImg" src="../../static/demo/datapic/1.jpg" mode="scaleToFill"></image>
			</swiper-item>
			<swiper-item>
				<image class="swiperImg" src="../../static/demo/datapic/2.jpg" mode="scaleToFill"></image>
			</swiper-item>
			<swiper-item>
				<image class="swiperImg" src="../../static/demo/datapic/3.jpg" mode="scaleToFill"></image>
			</swiper-item>
		</swiper>

		<!-- 进入众筹 -->
		<view class="bg-white u-f-ac u-f-jsb zhongchou">
			<view class="u-f-ac">
				<image style="width: 50upx;height: 50upx;border-radius: 100%;margin-right: 5upx;" src="../../static/demo/userpic/5.jpg"
				 mode="aspectFit"></image>
				<text style="font-weight: bold;font-size: 110%;">来众筹</text>
			</view>
			<view class="text-gray">查看全部<text class="cuIcon-right"></text></view>
		</view>

		<!-- 导航图标 -->
		<view class=" bg-white icon-father u-f-ac " style="margin-top: 10upx;">
			<view class="icon-item u-f1 " v-for="(item,index) in iconLists" :key="index">
				<view class="u-f-ajc">
					<image class="u-f-ajc" :src="item.url" mode="aspectFit"></image>
				</view>
				<view class="u-f-ajc">{{item.name}}</view>
			</view>
		</view>
		<!-- 特价商品 -->
		<view class="tejia bg-white">
			<view class="u-f-ac u-f-jsb" style="padding: 20upx 30upx;">
				<view class="u-f-ajc">
					<view class="u-f-ajc">
						<image 
						style="width: 50upx;height: 50upx;" 
						src="../../static/zcimg/qian.png"></image>
					</view>
					<view class="u-f-ajc text-bold"
					style="font-size: 120%;"
					>百亿补贴</view>
					<view class="u-f-ajc text-bold cu-tag radius">大牌正品 官方正品</view>
				</view>
				
				<view class="text-gray">
					全部<text class="cuIcon-right"></text>
				</view>
			</view>
		</view>
		<!-- 商品列表开始 -->
		<view class="u-f bg-white" style="padding: 20upx;">
			<view v-for="i in 5" :key="i"  class="u-f1">
				<view class="u-f-ajc" style="position: relative;">
					<image class="image1" 
					src="../../static/demo/demo11.jpg"></image>
					<view class="cu-tag radius sm bg-red" 
					style="position: absolute;bottom: 10upx;font-size: 80%;">
						超特价
					</view>
				</view>
				<view class="u-f-ajc" style="color: red;">
					<text style="font-size: 80%;">￥</text> 3999
				</view>
			</view>
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabIndex: 0,
				shu: null,
				search: "",
				TabList: [
					"热门", "数码", "蔬菜", "肉类", "众筹", "数码", "蔬菜", "肉类", "众筹"
				],
				iconLists: [{
						url: "../../static/zcimg/remen.png",
						name: "热卖众筹"
					},
					{
						url: "../../static/zcimg/ji.png",
						name: "家禽"
					},
					{
						url: "../../static/zcimg/rou.png",
						name: "鲜肉"
					},
					{
						url: "../../static/zcimg/shucai.png",
						name: "蔬菜"
					},
					{
						url: "../../static/zcimg/pingguo.png",
						name: "水果"
					}
				]
			}
		},
		methods: {
			qiehuan(index) {
				this.tabIndex = index
			}
		}
	}
</script>

<style scoped>
	page {
		background-color: #f7f7f7;
	}

	.swiperImg {
		width: 100%;
		height: 100%;
	}

	.zhongchou {
		height: 90upx;
		padding: 0 30upx;
	}

	.icon-item {}

	.icon-item image {
		width: 80upx;
		height: 80upx;
	}

	.icon-father {
		padding: 15upx 30upx;
	}

	.tejia {
		margin-top: 20upx;
	}
	.image1{
		width: 130upx;
		height: 130upx;
	}
</style>
