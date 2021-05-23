<template>
  <main v-if="!loading">
    <Title :text="title" :date="date" />
    <CountryMenu @getCountry="fetchCountryData" :countries="countries" />
    <DataCards :stats="stats" />

    <button
      class="bg-blue-800 text-sm font-medium leading-tight tracking-widest text-white hover:bg-blue-900 p-3 mt-8 mb-10 rounded focus:outline-none"
      @click="clearCountry"
    >
      <i class="far fa-times-circle"></i> Clear Country
    </button>
    <!-- Chart.js doesnt support vue 3 :( -->
    <!-- <Chart
      :chartData="arrConfirmed"
      :options="chartOptions"
      label="Confirmed"
    /> -->
    <Footer />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" />
    <Footer />
  </main>
</template>

<script>
import Title from "@/components/Title.vue";
import DataCards from "@/components/DataCards.vue";
import CountryMenu from "@/components/CountryMenu.vue";
import Footer from "@/components/Footer.vue";
// import Chart from "@/components/Chart.vue";
export default {
  name: "Home",
  components: {
    Title,
    DataCards,
    CountryMenu,
    Footer,
    // Chart,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      date: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/hourglass.gif"),
      arrConfirmed: [],
      arrRecovered: [],
      arrDeaths: [],
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
      },
    };
  },
  methods: {
    fetchData: async () => {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    fetchCountryData(country) {
      this.stats = country;
      this.title = country.Country;

      // Deleting the global object
      this.arrConfirmed.splice(0, 1);
      this.arrRecovered.splice(0, 1);
      this.arrDeaths.splice(0, 1);

      // pushing the country object
      this.arrConfirmed.push({
        date: this.date,
        total: this.stats.TotalConfirmed,
      });
      this.arrRecovered.push({
        date: this.date,
        total: this.stats.TotalRecovered,
      });
      this.arrDeaths.push({ date: this.date, total: this.stats.TotalDeaths });
    },
    async clearCountry() {
      this.loading = true;
      const data = await this.fetchData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const covidData = await this.fetchData();
    const { Date, Global, Countries } = covidData;
    this.date = Date;
    this.stats = Global;
    this.countries = Countries;
    this.loading = false;

    // chart
    this.arrConfirmed.push({
      date: this.date,
      total: this.stats.TotalConfirmed,
    });
    this.arrRecovered.push({
      date: this.date,
      total: this.stats.TotalRecovered,
    });
    this.arrDeaths.push({ date: this.date, total: this.stats.TotalDeaths });

    console.log(this.arrConfirmed);
  },
};
</script>
