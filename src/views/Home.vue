<template>
  <main v-if="!loading">
    <div class="flex flex-col align-center justify-center">
      <DataTitle :text="title" :dataDate="dataDate"/>
      <button
        @click="getGlobalData" 
        v-if="stats.Country"
        class="bg-green-500 font-semibold text-lg text-white rounded p-2 mb-8 focus:outline-none hover:bg-green-400">
        Worldwide stats 🌍
      </button> 
    </div>

    <DataBoxes :stats="stats" />
    <CountrySelect @get-country="getCountryData" :countries="countries" />
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <img :src="require('../assets/spinner.gif')" class="w-22 m-auto" alt="spinner gif">
    <div class="mt-6">
      <span class="bg-yellow-300 px-4 py-1 border-0 rounded-lg">
        Fetching data ...
      </span>
    </div>
  </main>
</template>

<script>
  import DataTitle from '@/components/DataTitle'
  import DataBoxes from '@/components/DataBoxes'
  import CountrySelect from '@/components/CountrySelect'

  export default {
    name: 'Home',
    components: {
      DataTitle,
      DataBoxes,
      CountrySelect
    },
    data () {
      return {
        loading: true,
        title: 'Worldwide',
        dataDate: '',
        stats: {},
        countries: []
      };
    },
    methods: {
      async fetchCovidData() {
        const res = await fetch('https://api.covid19api.com/summary');
        const data = await res.json();
        return data
      },
      getCountryData(country) {
        this.stats = country
        this.title = country.Country
      },
      async getGlobalData() {
        this.loading = true
        const data = await this.fetchCovidData();
        this.title = 'Worldwide'
        this.stats = data.Global
        this.loading = false
      }
    },
    async created() {
      const data = await this.fetchCovidData();
      this.dataDate = data.Date
      this.stats = data.Global
      this.countries = data.Countries
      this.loading = false
    }
  }
</script>
