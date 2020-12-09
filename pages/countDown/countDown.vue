<template>
	<view>
		<countDown :time="timeArr" />
	</view>
</template>

<script>
	import countDown from '../../components/countDown.vue'
	export default {
		components: {
			countDown
		},
		data() {
			return {
				// [开始时间,结束时间]
				timeArr: ['2020-12-05 12:00:00', '2020-12-12 12:00:00']
			};
		}
	}
</script>

<style lang="scss">

</style>
