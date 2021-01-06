<template>
	<view>
		<!-- 搜索框 -->
		<view class="cu-bar search bg-white">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input v-model="search" placeholder="请输入你想要的商品"></input>
				<text class="cuIcon-scan" style="font-size: 150%;"></text>
			</view>
		</view>
		<!-- 主体内容开始 -->
		<view class="u-f-ac">
			<scroll-view scroll-y style="height:calc(100vh - 200upx);width: 180upx;">
				<view @tap="select(i)" :style="{fontSize:selected == i?'120%':'100%'}" :class="selected == i?'bg-white text-bold':''"
				 class="type-item u-f-ajc" v-for="(p,i) in types" :key="i">
					<view v-if="selected==i" class="shuxian u-f-ac"></view>{{p}}
				</view>
			</scroll-view>
			<scroll-view class="bg-white u-f1" scroll-y style="height:calc(100vh - 200upx);">
				<view v-for="(p,i) in goods" :key="i">
					<view>{{types[i]}}</view>
					<view>
						<view v-for="(tp,ti) in p" :key="ti">
							<view>
								<image style="width: 100upx;height: 100upx;" :src="tp.url" mode="aspectFit"></image>
							</view>
							<view>{{tp.name}}</view>
							<view>{{tp.price}}</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>





	</view>
</template>

<script>
	export default {
		data() {
			return {
				search: "",
				types: [],
				goods: [],
				selected: 0
			}
		},
		onLoad() {
			this.gettypes();
			this.getgoods();
		},
		methods: {
			gettypes() {
				var data = [];
				for (var i = 0; i < 100; i++) {
					data.push('类目' + i)
				};
				this.types = data;
			},
			getgoods() {
				var data = [];
				for (var i = 0; i < 100; i++) {
					var p = [];
					p.push({
						url: "../../static/demo/userpic/15.jpg",
						name: this.types[i] + i,
						price: 1 * 2
					});
					p.push({
						url: "../../static/demo/userpic/16.jpg",
						name: this.types[i] + i,
						price: 1 * 2
					});
					p.push({
						url: "../../static/demo/userpic/17.jpg",
						name: this.types[i] + i,
						price: 1 * 2
					});
					data.push(p);
				};
				this.goods = data;
			},
			select(i) {
				this.selected = i;
			}
		}
	}
</script>

<style scoped>
	.type-item {
		height: 100upx;
		position: relative;
	}

	.shuxian {
		position: absolute;
		width: 5upx;
		height: 40upx;
		background-color: red;
		left: 5upx;
	}
</style>
