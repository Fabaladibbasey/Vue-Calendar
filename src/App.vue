<template>
	<main class="contianer w-3/4 m-auto mt-2">
		<h1 class="text-center mx-auto mb-3 text-3xl">
			Calendar
		</h1>
		<div class="w-4/5 flex justify-between p-2 mx-auto">
			<h4 class="text-3xl text-blue-700">{{ strMonth }}</h4>
			<h4 class="text-3xl text-blue-700">{{year}}</h4>
		</div>
		<section class="border-2 w-4/5 flex mx-auto">
			<p style="width: 14.29%;" class="border-2 w-2/3 text-center " v-for="day in days" :key="day">{{day}}</p>
		</section>
		<section class=" h-auto bg-gradient-to-tr from-blue-500 to-blue-600 w-4/5 flex mx-auto flex-wrap text-center place-items-center">
			<p style="width: 14.28%;" class="p-2" v-for="i in monthStartDay" :key="i">
			</p>
			<p style="width: 14.28%;" class="p-2 text-white " v-for="i in daysInMonth" :key="i"
				:class="{'bg-red-900' : getWeekDay(i) === 0, 'bg-yellow-400': isToday(i) }">
				{{i}}
			</p>
		</section>
		<div class="border-2 w-4/5 flex justify-between mx-auto">
			<button class="bg-gray-400 p-2 text-center border rounded capitalize mr-2 hover:bg-slate-400 transition-all"
				@click="previous">previous</button>
			<button
				class="bg-gray-400 p-2 text-center border rounded capitalize flex-auto hover:bg-slate-400 transition-all"
				@click="next">next</button>
		</div>
	</main>
</template>

<script>
import './assets/index.css'

export default {
  name: 'App',
  data(){
	return {
		days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
		year: new Date().getFullYear(),
		month: new Date().getMonth()
	}
  },
  computed: {
	daysInMonth() {

		return new Date(this.year, this.month + 1,  0).getDate();
	},
	strMonth(){
		return new Date(this.year, this.month).toLocaleString('en-us', {
			month: 'long'
		})
	},

	monthStartDay(){
		return new Date(this.year, this.month, 1).getDay()
	},

	// isToday(day){
	// 	return new Date().toDateString() === new Date(this.year, this.month, day).toDateString()
	// }
  },
  methods: {
	next(){
		this.month++
		if(this.month === 12){
			this.month = 0
			this.year++
		}
	},
	previous(){
		this.month--
		if (this.month === -1) {
			this.month = 11
			this.year--
		}
	},

	getWeekDay(day) {

		return new Date(this.year, this.month, day).getDay();
	},
	isToday(day){
		return new Date().toDateString() === new Date(this.year, this.month, day).toDateString()
	}
},
	components: {}
}
</script>

<style>

</style>
