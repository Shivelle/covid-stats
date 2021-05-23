<template>
  <div class="grid md:grid-cols-2 gap-4 xl:container">
    <div class="shadow-md bg-indigo-100 p-8 text-center rounded">
      <h3 class="text-2xl text-indigo-900 font-semibold mb-3">
        Cases
      </h3>
      <div class="text-lg mb-4">
        <span class="font-semibold text-indigo-900">{{ numberWithDots(stats.NewConfirmed) }}</span> new cases
      </div>
      <div class="text-lg mb-4">
        <span class="font-semibold text-indigo-900">{{ numberWithDots(stats.TotalConfirmed) }}</span> total cases
      </div>
    </div>
    <div class="shadow-md bg-red-100 p-8 text-center rounded">
      <h3 class="text-2xl text-red-900 font-semibold mb-3">
        Deaths
      </h3>
      <div class="text-lg mb-4">
        <span class="font-semibold text-red-900">{{ numberWithDots(stats.NewDeaths) }}</span> new deaths
      </div>
      <div class="text-lg mb-4">
        <span class="font-semibold text-red-900">{{ numberWithDots(stats.TotalDeaths) }}</span> total deaths
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'DataBoxes', 
    props: ['stats'], 
    methods: {
      numberWithDots(n) {
        return n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      }
    }
  }
</script>
