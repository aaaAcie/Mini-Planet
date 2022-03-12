<template>
	<view>
		<view class="header-box">
			<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="item in swiperAdList" :key="item.id">
					<navigator open-type="navigate" :url="'/pages/webview/webview?url=' + item.link">
						<image class="banner-swiper-img" :src="item.image" mode="aspectFill"></image>
					</navigator>
				</swiper-item>
			</swiper>
			<!-- 遮罩使用弧形框 -->
			<image id="crile" src="@/static/crile.png" mode="aspectFill" />
			<view class="card-header">
				<navigator url="/pages/feeds/feeds" open-type="switchTab" class="card-one card-left">
					<image class="img" src="@/static/coffee.png" mode="aspectFill"></image>
					<view class="text">精彩动态</view>
				</navigator>
				<navigator url="/pages/me/me" open-type="switchTab" class="card-one card-left">
					<image class="img" src="@/static/ran.png" mode="aspectFill"></image>
					<view class="text">个人中心</view>
				</navigator>
			</view>
		</view>
	</view>
</template>

<script>
	import { getAds } from '@/config/api.js'
	export default {
		data() {
			return {
				title: 'Hello',
				swiperAdList: []
			}
		},
		async onLoad() {
			this.getAdverts()
		},
		methods: {
			async getAdverts() {
				let adverts = await getAds()
				console.log(adverts)
				this.swiperAdList = adverts.map(item => {
					return {
						id: item.id,
						link: item.data.link,
						image: item.data.image
					}
				})
				console.log('swiperAdList== ',this.swiperAdList)
			},
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
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
	.header-box {
		position: relative;
		left: 0;
		height: 500upx;
		background-color: #f1f1f1;
		z-index: 1;
	
		// 广告位轮播器相关样式
		.swiper {
			width: 750upx;
			height: 400upx;
			position: absolute;
			left: 0;
			top: 0;
			text-align: center;
			z-index: 1;
	
			.banner-swiper-img {
				width: 750upx;
				height: 400upx;
				box-shadow: 0 0 2px 0 rgb(188, 188, 188);
			}
		}
	}
	#crile {
		width: 750upx;
		height: 50upx;
		position: absolute;
		left: 0;
		top: 355upx;
		z-index: 9;
	}
	.card-header {
		position: absolute;
		left: 0;
		top: 320upx;
		height: 160upx;
		z-index: 99;
		width: 710upx;
		margin-left: 20upx;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
		align-items: center;
		align-content: center;

		.card-one {
			width: 328upx;
			height: 96upx;
			border-radius: 49upx;
			background-color: #fff;
			margin: 0 10upx;
			box-shadow: 0 0 2px 0 rgb(188, 188, 188);
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			justify-content: flex-start;
			align-items: center;
			align-content: center;
		
			.img {
				width: 44upx;
				height: 44upx;
				margin-left: 50upx;
			}
		
			.iright {
				margin-left: 30upx;
				text-align: left;
				color: #888;
		
				.text {
					font-size: 30upx;
					color: #001432;
				}
		
				.iview {
					display: flex;
					flex-direction: row;
					flex-wrap: wrap;
					justify-content: space-between;
					align-items: center;
					align-content: center;
					font-size: 20upx;
					margin-top: -5upx;
				}
			}
		}
	}
</style>
