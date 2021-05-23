<template>
  <main v-if="!loading">
    Show data
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

  export default {
    name: 'Home',
    components: {},
    data () {
      return {
        loading: true,
        title: 'Global',
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
    },
    async created() {
      const data = await this.fetchCovidData();
      this.dataDate = data.dataDate
      this.stats = data.Global
      this.countries = data.countries
      this.loading = true
    }
  }
</script>
