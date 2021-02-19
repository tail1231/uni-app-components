<template>
	<view>
		<swiper class="swiper" previous-margin="87.5upx" next-margin='87.5upx' :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
			<swiper-item>
				<view class="swiper-item uni-bg-red">A</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">B</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">C</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: false,
				interval: 2000,
				duration: 500
			};
		}
	}
</script>

<style lang="scss">
	.swiper-item {
		margin: 0 auto;
		width: 500upx;
		background-color: #f00;
	}
</style>
