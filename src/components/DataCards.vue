<template>
  <div class="grid md:grid-cols-3 gap-4 mt-10">
    <!-- Card: Cases -->
    <div
      class="shadow-md bg-blue-100 p-8 text-center rounded transform hover:scale-105 transition-all ease-in-out duration-300"
    >
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Cases
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberFormat(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberFormat(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- Card: Recovered -->
    <div
      class="shadow-md bg-green-100 p-8 text-center rounded transform hover:scale-105 transition-all ease-in-out duration-300"
    >
      <h3 class="text-3xl text-green-900 font-bold mb-4">
        Recovered
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberFormat(stats.NewRecovered) }}
        <div class="text-2xl mb-4">
          <span class="font-bold">Total:</span>
          {{ numberFormat(stats.TotalRecovered) }}
        </div>
      </div>
    </div>
    <!-- Card: Deaths -->
    <div
      class="shadow-md bg-red-100 p-8 text-center rounded transform hover:scale-105 transition-all ease-in-out duration-300"
    >
      <h3 class="text-3xl text-red-900 font-bold mb-4">
        Deaths
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberFormat(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberFormat(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataCards",
  props: ["stats"],
  setup() {
    return {
      numberFormat(x) {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      },
    };
  },
};
</script>

<style></style>
