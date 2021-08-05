<template>
	<div class="text-white text-center mt-10">
		<div class="font-bold text-xl">
			{{ text }}
		</div>

		<div class="text-xl">{{ timeStamps }}</div>
	</div>
</template>


<script>
	import moment from "moment";
	export default {
		name: "Date",
		props: ["text", "Date"],

		computed: {
			timeStamps: function () {
				return moment(this.Date).format("MMMM Do YYYY, h:mm:ss a");
			},
		},
	};
</script>