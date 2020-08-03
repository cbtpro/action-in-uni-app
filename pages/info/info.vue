<template>
	<view class="news-info">
		<view class="news-info-title">{{news.title}}</view>
		<view class="news-info-created_at">{{news.created_at}}</view>
		<rich-text :nodes="news.content"></rich-text>
	</view>
</template>

<script>
export default {
	data() {
		return {
			news: {}
		}
	},
	onLoad(e) {
		const { newsid } = e
		uni.showLoading({
			title: 'Loading...',
			mask: false
		});
		uni.request({
			url: `https://unidemo.dcloud.net.cn/api/news/36kr/${newsid}`,
			method: 'GET',
			data: {},
			success: res => this.news = res.data,
			fail: () => {},
			complete: () => uni.hideLoading()
		});
	}
}
</script>

<style>
</style>
