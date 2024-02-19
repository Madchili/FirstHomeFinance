<script>
import SumUpComponent from './SumUpComponent.vue';

export default {
  components: {
    SumUpComponent
},
  data() {
    return {
      totals: [0, 0] // Array to hold the total from each SumList component
    };
  },
  computed: {
    combinedResult() {
      return this.totals[0] - this.totals[1];
    }
  },
  methods: {
    updateTotal(index, total) {
      // Update the total for the specified SumList component
      this.totals.splice(index, 1, total);
    }
  },

};
</script>

<template>
  <div>
    <SumUpComponent @updateTotal="updateTotal(0, $event)" title="Incomes"/>
    <SumUpComponent @updateTotal="updateTotal(1, $event)" title="Expenses"/>
    <h2>Combined Total: {{ combinedResult }}</h2>
  </div>
</template>
