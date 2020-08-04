<template>
	<view class="pass-time" @click="onClick">{{pastTime}}</view>
</template>

<script>
	export default {
		name: 'PastTime',
		props: {
			time: {
				type: [Number, String],
				default: 0,
				required: true
			},
			mode: {
				type: String,
				required: false,
				default: 'past'
			}
		},
		data() {
			return {
				pastTime: this.getPassTime()
			}
		},
		methods: {
			getPassTime() {
				let { mode, time } = this.$props
				if (mode === 'past') {
					let nowUtcTime = Date.now()
					let timeObj = new Date(time)
					let hhmm = timeObj.getHours() + ':' + timeObj.getMinutes()
					let utcTime = new Date(time).getTime()
					let pastMs = (nowUtcTime - utcTime) / 1000
					let pastDay = Math.floor(pastMs / 60*60*24)
					let result = ''
					if (pastMs < 60) result = '刚刚'
					else if (pastMs < 3600) result = Math.ceil(pastMs / 60) + '分钟前'
					else if (pastMs < 3600 * 12) result = Math.ceil(pastMs / 3600) + '小时前'
					else if (pastDay == 0) result = `今天${hhmm}`
					else if (pastDay == 1) result = `昨天${hhmm}`
					else if (pastDay == 2) result = `前天${hhmm}`
					else if (pastDay > 2 && pastDay < 16) result = pastDay + '天前'
					else result = this.time
					return result
				}
				return this.time
			},
			onClick(e) {
				console.log(this.time)
			}
		},
	}
</script>

<style>
</style>
