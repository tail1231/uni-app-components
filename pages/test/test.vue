<template>
	<view class="test">
		<view class="title">margin轮播</view>
		<view class="margin-swiper">
			<margin-swiper></margin-swiper>
		</view>
	</view>
</template>

<script>
	import MarginSwiper from '@/components/MarginSwiper.vue'
	export default {
		components: {
			MarginSwiper
		},
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.test {
		.title {
			text-align: center;
			font-size: 50upx;
			font-weight: 700;
		}
		.margin-swiper {
			
		}
	}
</style>
