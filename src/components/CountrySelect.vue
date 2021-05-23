<template>
  <h3 class="text-2xl font-semibold mt-10">Stats by country:</h3>
  <select 
    @change="onChange()"
    v-model="selected" 
    class="form-select mt-6 block w-full border p3 rounded">
    <option value="0" class="italic">Select Country</option>
    <option v-for="country in countries" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'], 
  data() {
    return {
      selected: 0
    }
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected)
      this.$emit('get-country', country)
    }
  }
}
</script>