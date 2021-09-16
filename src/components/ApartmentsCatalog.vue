<template>
  <div class="apartments-catalog">
    <ApartmentsFilters
      @show-apartments="showApartments"
    />
  </div>
</template>

<script>
import ApartmentsFilters from './ApartmentsFilters.vue'
export default {
  name: 'ApartmentsCatalog',
  components: {
    ApartmentsFilters
  },
  data() {
    return {
      filters: {},
    }
  },
  methods: {
    showApartments(values) {
      this.filters = values
    },
  }
}
</script>
