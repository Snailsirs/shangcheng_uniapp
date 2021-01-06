<template>
	<view>

		<view class="uni-tab-bar">
			<scroll-view scroll-x="true" class="uni-swiper-tab">
				<block v-for="(tab,index) in tabBars" :key="tab.id">
					<view class="swiper-tab-list" @tap="tabtap(index)" :class="{'active':tabIndex==index}">
						{{tab.name}}
						<view class="swiper-tab-line"></view>
					</view>
				</block>
			</scroll-view>
		</view>
		<swiper class="swiper-box" :style="{height:swiperheight+'px'}" 
		:current="tabIndex"
		@change="tabChange">
			<swiper-item v-for="(items,index) in newlist" :key="index">
				<scroll-view scroll-y="true" class="list">
					<block v-for="(item,index1) in items.list" :key="index1">
						<index-list :item="item" :index="index"></index-list>
					</block>
				</scroll-view>
			</swiper-item>
		</swiper>

	</view>

</template>

<script>
	import indexList from '../../components/index/index-list.vue'
	export default {
		components: {
			indexList
		},
		data() {
			return {
				swiperheight:"",
				tabIndex: 0,
				newlist: [{
						list: [{
								userpic: "../../static/demo/userpic/19.jpg",
								username: "昵称",
								isguanzhu: false,
								title: "我是标题",
								type: "img",
								titlepic: "../../static/demo/datapic/16.jpg",
								infonum: {
									index: 0, //0没有操作，1：顶，2：踩
									dingnum: 11,
									cainum: 11,
								},
								commentnum: 10,
								sharenum: 10,
							},
							{
								userpic: "../../static/demo/userpic/19.jpg",
								username: "昵称",
								isguanzhu: true,
								title: "我是标题",
								type: "video",
								titlepic: "../../static/demo/datapic/16.jpg",
								playnum: "20w",
								long: "2:47",
								infonum: {
									index: 1, //0没有操作，1：顶，2：踩
									dingnum: 11,
									cainum: 11,
								},
								commentnum: 10,
								sharenum: 10,
							}
						],
					},
					{
						list: []
					},
					{
						list: []
					},
					{
						list: []
					},
					{
						list: []
					},
					{
						list: []
					},
					{
						list: []
					}
				],

				tabBars: [{
					name: '关注',
					id: "guanzhu"
				}, {
					name: '推荐',
					id: "tuijian"
				}, {
					name: '体育',
					id: "tiyu"
				}, {
					name: '热点',
					id: "redian"
				}, {
					name: '财经',
					id: "caijing"
				}, {
					name: '娱乐',
					id: "yule"
				}, {
					name: '旅游',
					id: "lvyou"
				}],
			}
		},
		onLoad() {
			uni.getSystemInfo({
			    success:(res)=> {
			        // console.log(res.windowHeight);
					let height = res.windowHeight-uni.upx2px(-110);
					this.swiperheight = height;
			    }
			});
		},
		methods: {
			//滑动事件
			tabChange(e){
				this.tabIndex = e.detail.current 
			},
			// tabs通知swiper切换
			tabtap(index) {
				this.tabIndex = index;
				// this.swiperCurrent = index;
			}

		},
	}
</script>

<style scoped>
	.uni-swiper-tab {
		border-bottom: 1upx solid #EEEEEE;
	}

	.swiper-tab-list {
		color: #969696;
		font-weight: bold;
	}

	.uni-tab-bar .active {
		color: #343434;
	}

	.active .swiper-tab-line {
		border-bottom: 6upx solid #FEDE33;
		border-top: 6upx solid #FEDE33;
		border-radius: 20upx;
		width: 70upx;
		margin: auto;
	}

</style>
