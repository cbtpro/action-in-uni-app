<template>
	<view class="container">
		<view class="uni-list">
			<view class="list-cell" hover-class="list-cell-hover" v-for="(item, index) in newsList" :key="index" @click="newsClick" :data-newsid="item.post_id">
				<view class="news-list">
					<image :src="item.author_avatar" mode="scaleToFill" class="news-list-logo"></image>
					<view class="news-list-body">
						<view class="news-list-text-top">{{item.title}}</view>
						<view class="news-list-text-bottom uni-ellipsis">
							<past-time :time="item.created_at" mode="past"></past-time>
						</view>
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
				newsList: []
			}
		},
		onLoad() {
			uni.showLoading({
				title: 'Loading...',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					this.newsList = res.data
				},
				fail: () => {},
				complete: () => uni.hideLoading()
			});
		},
		methods: {
			newsClick(e) {
				const { newsid } = e.currentTarget.dataset
				uni.navigateTo({
					url: `../info/info?newsid=${newsid}`,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.news-list {
		display: inline-flex;
		line-height: 1.4rem;
	}
	.news-list-logo {
		width: 128upx;
		height: 128upx;
	}
	.news-list-body {
		flex: 1;
	}
	.news-list-text-bottom {
		color: gray;
	}
</style>
