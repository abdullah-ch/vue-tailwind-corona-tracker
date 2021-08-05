<template>
	<div>
		<main v-if="!loading">
			<Date :text="title" :Date="date" />
			<Cards :globalStatus="globalStatus" />
			<CountryPicker />
		</main>

		<main v-else class="flex flex-col justify-center align-center mt-10">
			<div class="">Fetching Data</div>
			<img :src="loadingImage" class="w-24" />
		</main>
	</div>
</template>

<script>
	import axios from "axios";
	import Date from "../components/Date.vue";
	import Cards from "../components/Cards.vue";
	import CountryPicker from "../components/CountryPicker.vue";
	export default {
		name: "Home",
		components: {
			Date,
			Cards,
			CountryPicker,
		},
		data() {
			return {
				loading: true,
				title: "Global",
				countries: [],
				globalStatus: {},
				date: "",
				loadingImage: require("../assets/hourglass.gif"),
			};
		},
		methods: {
			async fetchData() {
				const res = await axios.get("https://api.covid19api.com/summary");
				this.loading = false;
				return res.data;
			},
		},
		async created() {
			console.log("heloo");
			const data = await this.fetchData();
			console.log(data);
			(this.title = "Global"), (this.countries = data.Countries);
			this.date = data.Date;
			this.globalStatus = data.Global;
		},
	};
</script>
