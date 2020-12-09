<template>
	<view>
		{{`${leftTime.d}天 ${leftTime.h}时 ${leftTime.m}分 ${leftTime.s}秒`}}
	</view>
</template>

<script>
	import moment from 'moment'
	let dateFormat = "YYYY-MM-DD";
	export default {
		props: {
			time: {
				type: Array,
				default: []
			}
		},
		data() {
			return {
				startTime: '',
				endTime: '',
				leftTime: { //计时器：天/时/分/秒 
					d: 0,
					h: 0,
					m: 0,
					s: 0
				}
			};
		},
		created() {
			// this.startTime = moment(this.time[0]);
			this.startTime = moment();
			this.endTime = moment(this.time[1]);
			console.log('time', moment(this.time[0], dateFormat))
			this.timer = setInterval(() => {
				this.leftTime = this.leftDay()
			}, 1000);
		},
		methods: {
			leftDay() {
				const start = this.startTime;
				const end = this.endTime;
				if (start >= end) {
					if (this.timer) clearInterval(this.timer)
					return {
						d: 0,
						h: 0,
						m: 0,
						s: 0
					};
				}
				// console.log(moment(endTime).format("YYYY-MM-DD HH:mm:ss"));
				const d = end.diff(start, "day");
				const h = end.diff(start, "hour");
				const m = end.diff(start, "minute");
				const s = end.diff(start, "second");
				console.log('计时', `${ d}${ h - 24 * d } ${m - 60 * h} ${ s - 60 * m}`)
				return {
					d,
					h: h - 24 * d,
					m: m - 60 * h,
					s: s - 60 * m
				};
			},
		}
	}
</script>

<style lang="scss">

</style>
