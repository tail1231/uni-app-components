<template>
	<view>
		<swiper class="swiper" display-multiple-items="3" :indicator-dots="indicatorDots" :autoplay="autoplay"
		 :interval="interval" :duration="duration" circular @change="handleChange">
			<swiper-item v-for="(item,index) in list">
				<view class="swiper-item" :style="{
					opacity:getOpacity(index)
				}">{{item.text}} {{currentSwiper}}
					{{getOpacity(index)}}</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	// 750 - 150 = 600 除去中间元素
	// 600 / 2 = 300 剩余空间的一半
	// 300 - 150 = 150 减去需要露出的部分
	// 150 / 2 = 75
	// 75 + 150 = 225
	export default {
		data() {
			return {
				list: [{
						text: "A"
					},
					{
						text: "B"
					},
					{
						text: "C"
					},
					{
						text: "D"
					},
					{
						text: "E"
					},
					{
						text: "F"
					}
				],
				background: ['color1', 'color2', 'color3'],
				indicatorDots: false,
				autoplay: true,
				interval: 2000,
				duration: 500,
				currentSwiper: 0
			};
		},
		methods: {
			handleChange(e) {
				const {
					current
				} = e.detail;
				this.currentSwiper = current;
			}
		},
		computed: {
			// 使用计算属性，如果需要传参数，那就需要定义函数形式的计算属性，并且需要返回一个函数，参数要在该函数中去接收
			
			// 思路：
			// 1. 当前激活的swiper-item。不透明
			getOpacity() {
				return function(index) {
					if (this.currentSwiper == index) {
						return 1;
					}
					if (this.currentSwiper + 1 == index) {
						return 0.6;
					}
					if (this.currentSwiper + 2 == index) {
						return 0.3;
					}
					const l1 = this.currentSwiper - this.list.length;
					// console.log(this.currentSwiper)
					console.log(l1 , this.list.length ,index - 1);
					if (l1 == index - 1) {
						return 0.6;
					}
					if (l1 == index - 2) {
						return 0.3;
					}
					return 1;
				}
			}
		}
	}
</script>

<style lang="scss">
	.swiper-item {
		margin: 0 auto;
		width: 150upx;
		background-color: #f00;
	}
</style>
