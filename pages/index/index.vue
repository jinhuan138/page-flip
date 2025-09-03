<template>
	<view class="content">
		<view style="height: 80%; width: 80%;">
			<page-flip :papers="papers" />
		</view>
	</view>

</template>

<script>
export default {
	data() {
		return {
			papers: [],
		};
	},
	onLoad() {
		const baseurl = "/static/新人教初中七下生物(2022版课标修订)-图片";
		for (let i = 0; i <= 142; i++) {
			this.papers.push(`${baseurl}-${i}.jpg`);
		}
		console.log(this.papers);
	},
	methods: {},
};
</script>

<style>
.content {
	display: flex;
	align-items: center;
	justify-content: center;
	width: 100%;
	height: 100vh;
}

.logo {
	height: 200rpx;
	width: 200rpx;
	margin-top: 200rpx;
	margin-left: auto;
	margin-right: auto;
	margin-bottom: 50rpx;
}

.text-area {
	display: flex;
	justify-content: center;
}

.title {
	font-size: 36rpx;
	color: #8f8f94;
}
</style>
