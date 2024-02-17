<template>
  <div>
    <h2>{{ title }}</h2>

    <ul>
      <li v-for="(sum, index) in sums" :key="index">{{ sum }}</li>
    </ul>
    <input v-model="newSum" placeholder="Type sum here" @keyup.enter="addSum"/>
    <button @click="addSum">Add</button>
    <h3>Total: {{ total }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newSum: '',
      sums: []
    };
  },
  props: {
    title: {
      type: String,
      required: true,
      default: ''
    }
  },
  computed: {
    total() {
      return this.sums.reduce((acc, sum) => acc + parseFloat(sum), 0);
    }
  },
  methods: {
    addSum() {
      if (this.newSum.trim() !== '' && !isNaN(this.newSum)) {
        this.sums.push(this.newSum.trim());
        this.newSum = '';
        this.$emit('updateTotal', this.total); // Emit the total whenever a new sum is added
      }
    }
  },
  watch: {
    // Watch the total and emit its value whenever it changes
    total(newVal) {
      this.$emit('updateTotal', newVal);
    }
  }
};
</script>
