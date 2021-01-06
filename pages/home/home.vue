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
			<swiper-item v-for="(item,index) in banners" :key="index">
				<image class="swiperImg" :src="item.url" mode="scaleToFill"></image>
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
						<image style="width: 50upx;height: 50upx;" src="../../static/zcimg/qian.png"></image>
					</view>
					<view class="u-f-ajc text-bold" style="font-size: 120%;">百亿补贴</view>
					<view class="u-f-ajc text-bold cu-tag radius">大牌正品 官方正品</view>
				</view>

				<view class="text-gray">
					全部<text class="cuIcon-right"></text>
				</view>
			</view>
		</view>
		<!-- 商品列表开始 -->
		<view class="u-f bg-white" style="padding: 20upx;">
			<view v-for="(item,index) in tejiaLists" :key="index" class="u-f1">
				<view class="u-f-ajc" style="position: relative;">
					<image class="image1" :src="item.url"></image>
					<view class="cu-tag radius sm bg-red" style="position: absolute;bottom: 10upx;font-size: 80%;">
						{{item.tag}}
					</view>
				</view>
				<view class="u-f-ajc" style="color: red;">
					<text style="font-size: 80%;">￥</text> {{item.price}}
				</view>
			</view>
		</view>
		<!-- 商品列表 -->
		<view style="margin-top: 30upx;padding: 0 30upx;">
			<view v-for="(item,index) in goodsLists" :key="index" class="u-f u-f-jsa bg-white" style="border-bottom: 1upx solid #e7e7e7;padding: 20upx 0;">
				<view style="width: 250upx;">
					<image style="width: 250upx;height: 250upx;" 
					:src="item.url"></image>
				</view>
				<view style="width: 400upx;" class="u-f u-f-column u-f-jsb">
					<view class="">
						<view style="font-weight: bold;font-size: 110%;">
							<text v-if="item.tag1==true" class="cu-tag sm bg-gradual-orange round">女神节</text>
							{{item.title}}
						</view>
						<view class="cu-tag bg-brown radius">
							{{item.shop}}
						</view>
					</view>
					<view>
						<view>
							<text v-if="item.tag2" class="cu-tag sm bg-red radius">小编推荐</text>
							<text v-if="item.tag3" class="cu-tag sm bg-orange radius">假一赔十</text>
						</view>
						<view style="font-size: 120%;">
							<text style="color: red;font-size: 120%;">￥{{item.price}}</text>
							<text style="color: grey;font-size: 80%;">已买{{item.num}}+</text>
						</view>
						<view style="width: 100%;height: 20upx;"></view>
					</view>
				</view>
			</view>
		</view>



	</view>
</template>

<script>
	export default {
		data() {
			return {
				banners: [],
				tabIndex: 0,
				shu: null,
				search: "",
				iconLists: [],
				tejiaLists:[],
				goodsLists:[],
				TabList: [
					"热门", "数码", "蔬菜", "肉类", "众筹", "数码", "蔬菜", "肉类", "众筹"
				]
			}
		},
		onLoad() {
			this.getbanners();
			this.geticonLists();
			this.gettejia();
			this.getgoodsLists();
		},
		methods: {
			qiehuan(index) {
				this.tabIndex = index
			},
			getbanners() {
				var data = [{
						url: "../../static/demo/datapic/1.jpg",
						actiion: ""
					},
					{
						url: "../../static/demo/datapic/2.jpg",
						actiion: ""
					},
					{
						url: "../../static/demo/datapic/3.jpg",
						actiion: ""
					}
				];
				this.banners = data
			},
			geticonLists() {
				var data = [{
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
				];
				this.iconLists = data
			},
			gettejia() {
				var data = [];
				for(var i=0;i<5;i++){
					var p = {
						id: "1",
						url: "../../static/demo/demo101.jpg",
						price: "",
						tag:"特价"
					};
					p.tag+=i;
					p.id=i+1;
					p.price+=i;
					data.push(p);
				};
				this.tejiaLists = data;
			},
			getgoodsLists(){
				var data = [];
				for(var i=0;i<10;i++){
					var p = {
						id: "1",
						title:"小米震撼发布3999！！",
						tag1:true,
						shop:"黑板教育旗舰店",
						tag2:true,
						tag3:true,
						url:"../../static/zcimg/remen.png",
						price:3999,
						num:1000
					};
					data.push(p);
				};
				this.goodsLists = data;
			}
		}
	}
</script>

<style scoped>
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

	.image1 {
		width: 130upx;
		height: 130upx;
	}
</style>
