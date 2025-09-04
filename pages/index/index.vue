<template>
	<view class="content">
		<view style="height: 80%; width: 80%;">
			<page-flip :papers="papers" @pageChange="pageChange"/>
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
	mounted() {
		const baseurl = "https://raw.githubusercontent.com/jinhuan138/page-flip/main/static/新人教初中七下生物(2022版课标修订)-图片";
		for (let i = 0; i <= 10; i++) {
			this.papers.push(`${baseurl}-${i}.jpg`);
		}
		console.log(this.papers);
	},
	methods: {
		pageChange(page) {
			console.log("当前页码", page);
		},
	},
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

</style>
