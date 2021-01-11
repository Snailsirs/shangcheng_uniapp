<template>
	<view>
		<!-- 头部 -->
		<view class="caozuo u-f-ac u-f-jsb">
			<view>
				<checkbox-group @change="changeAll">
					<checkbox class="round red" :class="checked==true?'checked':''" :checked="checked" style="transform:scale(0.7);">
					</checkbox>
					<text style="font-size: 110%;margin-left: 10upx;">全选</text>
				</checkbox-group>

			</view>
			<view>
				<view @tap="deleteAll" class="cu-btn sm round">
					<text class="cuIcon-delete"></text>
					删除
				</view>
			</view>
		</view>

		<!-- 主体部分 -->
		<view class="cart-content">
			<view v-for="(p,i) in lists" :key="i" class="cart-item bg-white u-f-ac">
				<view class="u-f-ajc" style="width: 240upx;">
					<checkbox-group>
						<checkbox @tap="changeChecked(i)" class="round red" :class="p.checked==true?'checked':''" :checked="p.checked"
						 style="transform:scale(0.7);">
						</checkbox>
					</checkbox-group>
					<image :src="p.img" mode="widthFix"></image>
				</view>
				<view class="u-f1 cart-item-right">
					<view class="cart-title">{{p.title}}</view>
					<view>
						<view class="text-gray">类型:{{p.type}}</view>
						<view class="u-f-ac u-f-jsb">
							<view class="text-red text-bold text-lg">￥{{p.price}}</view>
							<uni-number-box @change="changejishu" v-model="p.num" :min="0" :max="9999"></uni-number-box>
						</view>
					</view>

				</view>
			</view>
		</view>

		<!-- 底部 -->
		<view class="heji u-f-ac u-f-jsb">
			<view style="font-size: 110%;">合计: ￥
				<text class="text-orange">{{sum}}</text>
			</view>
			<view>
				<view class="cu-btn bg-gradual-red round">去结算</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniNumberBox from "../../components/uni-number-box/uni-number-box.vue"
	export default {
		components: {
			uniNumberBox
		},
		data() {
			return {
				checked: false,
				lists: []
			}
		},
		onLoad(e) {
			this.getdata();
			// var pages = getCurrentPages();
			// var page = pages[pages.length - 1];
			// var webview = page.$getAppWebview();

			// webview.setStyle({
			// 	titleNView: {
			// 		backgroundImage: "linear-gradient(to right,#73ADF8,#3081FF)"
			// 	}
			// });
		},
		computed: {
			sum() {
				var he = 0;
				this.lists.forEach(p => {
					if (p.checked == true) {
						he += p.num * p.price;
					}
				});
				return he;
			}
		},
		methods: {
			deleteAll() {
				this.lists = this.lists.filter(p => {
					return !p.checked;
				})

			},
			changeChecked(index) {
				this.lists[index].checked = !this.lists[index].checked;
				var selected = this.lists.filter(p => {
					return !p.checked
				});
				selected.length == 0 ? this.checked = true : this.checked = false;

			},
			changejishu(val) {
				val = parseInt(val);
				if (val == 0) {
					var thisdata = this.lists.find((p) => {
						return p.num == 0;
					});
					var that = this;
					uni.showModal({
						confirmText: "是的",
						content: "您确定移除" + thisdata.title,
						title: "删除警告",
						success(res) {
							if (res.confirm) {
								that.lists = that.lists.filter(p => {
									return p.id != thisdata.id;
								})
							}
						}
					})
				}
			},
			changeAll(e) {
				this.lists.forEach(p => {
					p.checked = !this.checked;
				});
				this.checked = !this.checked;
				// this.checked ? this.checked = false : this.checked = true
			},
			getdata() {
				var data = [{
						id: 1,
						img: "../../static/demo/topicpic/11.jpeg",
						title: "标题1 震撼版",
						type: "珍珠白",
						price: 999,
						num: 1,
						checked: true
					},
					{
						id: 2,
						img: "../../static/demo/topicpic/12.jpeg",
						title: "标题2 青春版",
						type: "磨砂黑",
						price: 999,
						num: 10,
						checked: true
					},
					{
						id: 3,
						img: "../../static/demo/topicpic/13.jpeg",
						title: "标题3 清凉夏日版，10年震撼大作",
						type: "高贵红",
						price: 999,
						num: 1,
						checked: true
					}
				];
				this.lists = data;
			}
		}
	}
</script>

<style scoped>
	.caozuo {
		position: fixed;
		top: 0upx;
		/*#ifdef H5*/
		top: 90upx;
		/*#endif*/
		background-color: white;
		width: 100%;
		height: 100upx;
		padding: 0 20upx;
	}

	>>>.uni-checkbox-input:hover {
		border-color: #CCCCCC !important;
	}

	.cart-content {
		margin: 120upx 0 200upx;

	}

	.cart-item {
		padding: 20upx;
		margin-top: 30upx;
		width: 100%;
		height: 200upx;
	}

	.cart-item image {
		margin-left: 10upx;
	}

	.cart-item-right {
		width: 100%;
		height: 100%;
		padding: 0 20upx 0 60upx;
	}

	.cart-title {
		width: 200px;
		font-size: 110%;
		font-weight: bold;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.heji {
		position: fixed;
		bottom: 0upx;
		/*#ifdef H5*/
		bottom: 100upx;
		/*#endif*/
		bottom: 100upx;
		width: 100%;
		height: 100upx;
		background-color: white;
		padding: 0 30upx;
	}
</style>
