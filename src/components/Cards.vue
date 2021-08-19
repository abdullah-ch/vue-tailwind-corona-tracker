<template>
  <div class="flex flex-col md:flex-row mt-5 justify-center items-center">
    <!-- Box One -->
    <div
      class="
				flex flex-col
				rounded
				bg-white
				w-52
				md:w-64
				border-b-8 border-yellow-500
				mb-6
				pl-2
				md:mr-5
			"
    >
      <h3 class="text-gray-500 text-xl md:text-2xl">Cases</h3>
      <span class="text-black text-xl md:text-2xl pb-5 pt-5"
        >New: {{ commaSeparatedStatus(globalStatus.NewConfirmed) }}</span
      >
      <span class="text-gray-black text-xl md:text-2xl"
        >Total : {{ commaSeparatedStatus(globalStatus.TotalConfirmed) }}
      </span>
    </div>
    <!-- Box Two -->
    <div
      class="
				flex flex-col
				rounded
				bg-white
				w-52
				md:w-64
				border-b-8 border-red-800
				mb-6
				pl-2
			"
    >
      <h3 class="text-gray-500 text-xl md:text-2xl">Deaths</h3>
      <span class="text-black text-xl md:text-2xl pb-5 pt-5"
        >New: {{ commaSeparatedStatus(globalStatus.NewDeaths) }}</span
      >
      <span class="text-gray-black text-xl md:text-2xl"
        >Total : {{ commaSeparatedStatus(globalStatus.TotalDeaths) }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cards",
  props: ["globalStatus"],
  methods: {
    commaSeparatedStatus(data) {
      return data.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>
