<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="rich-text" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:"",
				strings:""
			};
		},
		onLoad(e) {
			console.log(e);
			uni.showLoading({
				title: '加载中...',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					uni.hideLoading();
					console.log('info->',res);
					this.title = res.data.title;
					this.strings = res.data.content;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.content{
	padding: 10upx 10upx;
	width:730upx;
	flex-wrap:wrap;
}
.title{
	font-size: 32upx;
	font-weight: 600;
	padding: 2upx;
}
.art-content{
	width:720upx;
	padding: 15upx;
	line-height: 33upx;
}
</style>
