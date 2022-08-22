<template>
	<view>
		<u-notice-bar :text="notice" mode="closable" speed=60></u-notice-bar>


		<view class="u-demo-block">
			<u-gap bgColor="transparent" height="15"></u-gap>
			<u-swiper @click="NavWeb" :list="list4" keyName="image" circular @change="e => currentNum = e.current"
				:autoplay="true" indicatorStyle="right: 20px">
				<view slot="indicator" class="indicator-num">
					<text class="indicator-num__text">{{currentNum+1}}/{{ list4.length }}</text>
				</view>
			</u-swiper>
		</view>



		<view v-for="(v, k) in items" :key="k">
			<view style="background-color:aqua; padding: 10rpx; display: flex;">
				<u-icon name="shopping-cart-fill" size=20></u-icon>
				<text style="margin-left: 10rpx;">{{v.title}}</text>
			</view>

			<swiper :indicator-dots="true" class="swiper">
				<swiper-item>
					<u-grid :border="true" :col="2">
						<u-grid-item :customStyle="{width:375+'rpx',height:300+'rpx'}" v-for="(item, index) in baseList"
							:index="index" :key="index">
							<image style="width: 240rpx; height: 300rpx;" :src="baseURL + item.name" mode=""></image>
							<view>
								<view>{{item.title}}</view>
							</view>
						</u-grid-item>
					</u-grid>
				</swiper-item>
				<swiper-item>
					<u-grid :border="true" :col="2">
						<u-grid-item :customStyle="{width:375+'rpx',height:300+'rpx'}" v-for="(item, index) in baseList"
							:index="index" :key="index">
							<image style="width: 240rpx; height: 300rpx;" :src="baseURL + item.name" mode=""></image>
							<view>
								<view>{{item.title}}</view>
							</view>
						</u-grid-item>
					</u-grid>
				</swiper-item>
				<swiper-item>
					<u-grid :border="true" :col="2">
						<u-grid-item :customStyle="{width:375+'rpx',height:300+'rpx'}" v-for="(item, index) in baseList"
							:index="index" :key="index">
							<image style="width: 240rpx; height: 300rpx;" :src="baseURL + item.name" mode=""></image>
							<view>
								<view>{{item.title}}</view>
							</view>
						</u-grid-item>
					</u-grid>
				</swiper-item>
			</swiper>
		</view>

		<u-grid :col="4" :showBorder="false">
			<u-grid-item v-for="(item, index) in icons" :key="index">
				<view
					style="display: flex; flex-direction: column; justify-content: space-around; align-items: center;">
					<image :src="item.icon" style="width: 50rpx; height: 50rpx;" mode=""></image>
					<text style="color: gray;">{{ item.title }}</text>
				</view>
			</u-grid-item>
		</u-grid>

		<view v-if="showGoTop" class="gotop" @click="gotoTop" hover-class="gotop-active">↑</view>
	</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiperList: ['kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'],
				baseURL: 'https://ptu.zbmwd.top/image/',
				showGoTop: false,
				data: null,
				baseList: [{
						name: 'a.jpg',
						title: '图片1'
					},
					{
						name: 'wallhaven-3zv5pd.jpg',
						title: '锁头2'
					},
					{
						name: 'wallhaven-g769jq.jpg',
						title: '星星3'
					},
					{
						name: 'wallhaven-57vk17.jpg',
						title: '星星4'
					},
				],
				currentNum: 0,
				list4: [
					{
						id: 1,
						image: 'https://ptu.zbmwd.top/image/wallhaven-57vk17.jpg',
						name: "wallhaven-57vk17.jpg"
					},
					{
						id: 2,
						image: 'https://ptu.zbmwd.top/image/wallhaven-k7eko6.jpg',
						name: "wallhaven-k7eko6.jpg"
					},
					{
						id: 3,
						image: 'https://ptu.zbmwd.top/image/wallhaven-y86gzx.jpg',
						name: "wallhaven-y86gzx.jpg"
					},
				],
				// #ifdef H5
				notice: '欢迎使用 UniApp , 这里是 h5 页面。'
				// #endif

				// #ifdef MP
				notice: '欢迎使用 UniApp , 这里是 小程序 页面。',
				// #endif

				// #ifdef APP-PLUS
				notice: '欢迎使用 UniApp , 这里是 App 页面。'
				// #endif
			};
		},
		methods: {
			gotoTop() {
				uni.pageScrollTo({
					scrollTop: 0,
					success: () => {
						this.showGoTop = false;
					}
				})
			},
			NavWeb(index) {
				let name = this.list4[index].name
				uni.navigateTo({
					url: `../webview/webview?name=${name}`,
					success: res=>{
						console.log(res);
					},
					fail: res=>{
						console.log(res);
					}
				})
			},
		},
		onReachBottom() {
			this.showGoTop = true;
		},
		computed: {
			items() {
				return [{
						title: '1F/首页推荐',
					},
					{
						title: '2F/热销单品',
					},
					{
						title: '3F/最新上架',
					}
				]
			},
			icons() {
				return [{
						title: '品质保障',
						icon: '../../static/icons/icon1.png'
					},
					{
						title: '私人订制',
						icon: '../../static/icons/icon2.png'
					},
					{
						title: '学员特供',
						icon: '../../static/icons/icon3.png'
					},
					{
						title: '专属特权',
						icon: '../../static/icons/icon4.png'
					}
				];
			}
		}
	};
</script>

<style lang="scss">
	.swiper {
		height: 700rpx;
	}

	.gotop {
		position: fixed;
		bottom: 80px;
		right: 10px;
		background-color: rgba(2, 196, 255, 0.5);
		font-size: 2em;
		border-radius: 50%;
		width: 100rpx;
		height: 100rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.gotop-active {
		opacity: 0.7;
	}
</style>
