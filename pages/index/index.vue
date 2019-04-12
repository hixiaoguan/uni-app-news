<template>
	<view class="content">
        <view class="uni-list">
        	<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" :data-newsid="item.post_id" @tap="openinfo">
        		<view class="uni-media-list">
        			<image class="uni-media-list-logo" :src="item.author_avatar"></image>
        			<view class="uni-media-list-body">
        				<view class="uni-media-list-text-top">{{item.title}}</view>
        				<view class="uni-media-list-text-bottom uni-ellipsis">{{item.created_at}}</view>
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
				news: []
			}
		},
		methods:{
			openinfo(e){
				// console.log('id->',e.currentTarget.dataset.newsid);
				var newsid = e.currentTarget.dataset.newsid;
				uni.navigateTo({
					url: '../info/info?newsid='+newsid
				});
			}
		},
		onLoad() {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					// console.log(res);
					this.news = res.data;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.uni-media-list-body{
		height: auto;
	}
	.uni-media-list-text-top{
		line-height: 40upx;
	}
</style>
