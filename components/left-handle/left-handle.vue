<template>
	<view class="left-handle">
		<view class="left-content" @touchstart="handleTouchStart" @touchmove="handleTouchMove"
			@touchend="handleTouchEnd">
			<slot></slot>
		</view>
		<view class="skate" :style="{ right: r + 'px' , width : w + 'px'}"></view>


	</view>
</template>

<script>
	export default {
		name: "left-handle",
		data() {
			return {
				r: -60, // 滑块的位置
				w: 60, // 滑块的宽度
				startX: undefined, // 触摸开始的位置
				distance: 0, // 滑动距离
			};
		},
		methods: {
			// 触摸
			handleTouchStart(e) {
				console.log('touchstart', e)
				this.startX = e.touches[0].clientX;
			},
			// 滑动
			handleTouchMove(e) {
				console.log('touchmove', e)
				let {
					startX,
					r
				} = this;
				// 计算移动的距离
				let sub = e.touches[0].clientX - startX;
				let abs = Math.abs(e.touches[0].clientX - startX);
				console.log('距离', sub)
				this.distance = abs;
				// 小于0 左移
				if (sub < 0) {
					this.r = this.r - sub;
				} else { // 右移
					
				}
				if (r >= 0) {
					this.r = 0;
					this.w = abs;
				}
			},
			// 触摸离开
			handleTouchEnd(e) {
				console.log('宽度', this.w)
				let {
					w,
					distance
				} = this;

				if (w >= 40) {
					this.w = 60;
				} else if (w < 40 || distance < 40) {
					this.w = 0;
				}
				console.log('touchend', e)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.left-handle {
		position: relative;
		width: 100%;
		height: 100%;
		overflow: hidden;

		.left-content {
			height: 100%;
			background-color: #f0f;
		}

		.skate {
			position: absolute;
			top: 0;
			right: -60px;
			width: 60px;
			height: 100%;
			background-color: aqua;
		}
	}
</style>
