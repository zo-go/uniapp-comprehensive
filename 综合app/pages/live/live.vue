<template>
	<view>
		<uni-collapse v-if="cates">
			<uni-collapse-item :title="cates[current].cate_name">
				<view style="background-color: white;">
					<uni-tag @click="chooseCate(index)" style="margin: 10rpx;" v-for="(item,index) in cates"
						:text="item.cate_name" :type="index==current? 'error':'primary'"></uni-tag>
				</view>

			</uni-collapse-item>
		</uni-collapse>

		<uni-grid :column="3" :showBorder="false" :square="false" :highlight="false">
			<uni-grid-item v-for="(item,index) in rooms">
				<navigator
					:url="`/pages/room-detail/room-detail?short_name=${item.short_name}&tag_name=${item.tag_name}`"
					style="display: flex; flex-direction: column; margin-top: 15rpx; align-items: center;">
					<image :src="item.icon_name" style="width: 220rpx; height: 220rpx;" mode=""></image>
					<text>{{item.tag_name}}</text>
				</navigator>
			</uni-grid-item>

		</uni-grid>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates: null,
				current: 1,
				rooms: []
			}
		},
		mounted() {
			this.getCates()
		},
		methods: {
			chooseCate(index) {
				this.current = index;

				this.getRooms(index)
			},
			getRooms(index) {
				const shortName = this.cates[index].short_name;

				uni.request({
					url: 'http://capi.douyucdn.cn/api/v1/getColumnDetail',
					method: 'GET',
					data: {
						shortName: shortName
					},
					success: res => {
						console.log(res);

						this.rooms = res.data.data;
					},
					fail: () => {},
					complete: () => {}
				});
			},
			getCates() {
				uni.request({
					url: 'http://capi.douyucdn.cn/api/v1/getColumnList',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res);
						this.cates = res.data.data

						this.getRooms(1)
					},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>

</style>
