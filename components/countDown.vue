<template>
	<view>
		{{`${leftTime.d}天 ${leftTime.h}时 ${leftTime.m}分 ${leftTime.s}秒`}}
	</view>
</template>

<script>
	import moment from 'moment'
	let dateFormat = "YYYY-MM-DD HH:mm:ss";
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
			this.startTime = moment().format(dateFormat);
			this.endTime = moment(this.time[1]).format(dateFormat);
			this.timer = setInterval(() => {
				this.leftTime = this.leftDay()
			}, 1000);
		},
		methods: {
			leftDay() {
				const start = this.startTime;
				const end = this.endTime;
				console.log(start,end)
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
				const d = moment(end).diff(moment(start), "day");
				const h = moment(end).diff(moment(start), "hour");
				const m = moment(end).diff(moment(start), "minute");
				const s = moment(end).diff(moment(start), "second");
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
