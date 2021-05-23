<template>
  <select
    v-model="selected"
    class="form-select block w-full border p-3 mt-10"
    @change="changeStats()"
  >
    <option value="0">Select Country</option>
    <option
      v-for="(country, index) in countries"
      :key="index"
      :value="country.ID"
    >
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountryMenu",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    changeStats() {
      const country = this.countries.find((c) => c.ID === this.selected);
      this.$emit("getCountry", country);
    },
  },
};
</script>

<style></style>
