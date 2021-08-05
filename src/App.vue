
<template >
	<div>
		<Header />

		<main v-if="!loading">
			<Date :text="title" :Date="date" />
			<Cards :globalStatus="globalStatus" />
			<CountryPicker @getCountry="getCountryData" :countries="countries" />
		</main>

		<main
			v-else-if="loading"
			class="flex flex-col justify-center items-center mt-10"
		>
			<div class="text-white md:text-2xl mb-5">Fetching Data</div>
			<img :src="loadingImage" class="w-24" />
		</main>
	</div>
</template>


<script>
	import axios from "axios";
	import Header from "./components/Header.vue";
	import Date from "./components/Date.vue";
	import Cards from "./components/Cards.vue";
	import CountryPicker from "./components/CountryPicker.vue";
	export default {
		components: { Header, Date, Cards, CountryPicker },
		data() {
			return {
				loading: true,
				title: "Global",
				countries: [],
				globalStatus: {},
				date: "",
				loadingImage: require("./assets/hourglass.gif"),
			};
		},
		methods: {
			async getGlobalData() {
				this.loading = true;
				const data = await this.fetchData();
				this.loading = false;
				this.title = "Global";
				this.date = data.Date;
				this.globalStatus = data.Global;
			},
			getCountryData(country) {
				console.log("emitted country is", country);
				if (typeof country == "undefined") {
					this.getGlobalData();
				} else {
					this.globalStatus = country;
					this.title = country.Country;
					this.date = country.Date;
				}
			},
			async fetchData() {
				const res = await axios.get("https://api.covid19api.com/summary");
				return res.data;
			},
		},
		async created() {
			const data = await this.fetchData();
			this.loading = false;
			(this.title = "Global"), (this.countries = data.Countries);
			this.date = data.Date;
			this.globalStatus = data.Global;
		},
	};
</script>
