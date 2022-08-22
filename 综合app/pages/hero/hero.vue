<template>
	<view style="display: flex;">
		<scroll-view scroll-y style="width: 250rpx; background-color: #EEE;" :style="{ height: winHeight }">
			<view @click="chooseItem(index)" :class="{ cur: current == index }" style="padding: 10rpx;"
				v-for="(item, index) in hero">
				{{ item.title }}
			</view>
		</scroll-view>

		<scroll-view>
			<view style="width: 500rpx;padding: 10px; display: flex;">
				<image style="width: 200rpx;height: 200rpx;"
					:src="`https://game.gtimg.cn/images/lol/act/img/champion/${detail.hero.alias}.png`"></image>
				<view style="margin-left: 10rpx; display: flex; flex-direction: column; justify-content: space-evenly;">
					<view style="font-size: 1.2em;">{{ detail.hero.title }}</view>
					<view>昵称: {{ detail.hero.name }}</view>
					<view>金币: {{ detail.hero.goldPrice }}</view>
					<view>点券: {{ detail.hero.couponPrice }}</view>
				</view>
			</view>

			<!-- 背景故事 -->
			<uni-card title="背景故事" isShadow isFull>
				<view style="font-size: 0.8em;">{{ detail.hero.shortBio }}</view>
			</uni-card>

			<uni-collapse accordion>
				<uni-collapse-item title="使用建议" showAnimation>
					<uni-list>
						<uni-list-item v-for="(item, index) in detail.hero.allytips" :key="index" :title="item">
						</uni-list-item>
					</uni-list>
				</uni-collapse-item>

				<uni-collapse-item title="对战技巧" showAnimation>
					<uni-list>
						<uni-list-item v-for="(item, index) in detail.hero.enemytips" :key="index" :title="item">
						</uni-list-item>
					</uni-list>
				</uni-collapse-item>

				<uni-collapse-item title="技能" showAnimation>
					<uni-list>
						<uni-list-item direction="column" v-for="(item, index) in detail.spells" :key="index"
							:title="item.name" :thumb="item.abilityIconPath" thumbSize="lg" :note="item.description">
						</uni-list-item>
					</uni-list>
				</uni-collapse-item>

				<uni-collapse-item title="皮肤" showAnimation>
					<uni-list>
						<uni-list-item v-for="(item, index) in detail.skins" :key="index" :title="item.name"
							:thumb="item.iconImg" thumbSize="lg"></uni-list-item>
					</uni-list>
				</uni-collapse-item>
			</uni-collapse>

		</scroll-view>
	</view>


</template>

<script>
	export default {
		data() {
			return {
				hero: [],
				current: 0,
				detail: null,
				showRight: true,
				indicator: true
			};
		},
		mounted() {
			this.getMenu();
		},
		methods: {
			getMenu() {
				uni.request({
					url: 'https://game.gtimg.cn/images/lol/act/img/js/heroList/hero_list.js',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res);

						this.hero = res.data.hero;

						this.getDetail(0);
					},
					fail: () => {},
					complete: () => {}
				});

			},
			chooseItem(index) {
				this.current = index;
				this.getDetail(index);
			},
			getDetail(index) {
				const hid = this.hero[index].heroId;

				uni.request({
					url: `https://game.gtimg.cn/images/lol/act/img/js/hero/${hid}.js`,
					method: 'GET',
					data: {},
					success: res => {
						console.log(res);

						this.detail = res.data;
					},
					fail: () => {},
					complete: () => {}
				});
			}
		},
		computed: {
			winHeight() {
				return uni.getSystemInfoSync().windowHeight + 'px';
			}
		}
	};
</script>

<style>
	.cur {
		color: orange;
		border-bottom: 2px solid orange;
	}
</style>
