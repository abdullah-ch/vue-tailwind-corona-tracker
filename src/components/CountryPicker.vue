<template>
  <div class="flex justify-center">
    <select @change="onChange()" v-model="selected" class="w-auto mt-2">
      <option value="0" default>Global</option>
      <option
        v-for="(country, index) in countries"
        :key="index"
        :value="country.ID"
      >
        {{ country.Country }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "CountryPicker",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find(
        (country) => country.ID === this.selected
      );

      this.$emit("getCountry", country);
    },
  },
};
</script>
