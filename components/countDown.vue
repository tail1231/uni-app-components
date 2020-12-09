<template>
	<view>
		{{cutDown}}
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
				},
				cutDown: ""
			};
		},
		created() {
			setInterval(() => {
				let start = moment(new Date()); //获取开始时间
				let end = moment(new Date("2020/12/10")); //结束时间
				let diff = end.diff(start); //时间差
				let time =
					`${end.diff(start,'day')}天${moment.duration(diff).hours()}小时${moment.duration(diff).minutes()}分${moment.duration(diff).seconds()}秒` //格式化为需要的格式 这里是时分秒
				this.cutDown = time
				console.log(time)
			}, 1000)
		},
		methods: {
			leftDay() {
				const start = this.startTime;
				const end = this.endTime;
				console.log(start, end)
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
