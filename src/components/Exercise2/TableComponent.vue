<template>
  <div class="flex flex-col">
    <!-- <p>{{ JSON.stringify(records) }}</p> -->

    <table class="min-w-full divide-y divide-gray-200 dark:divide-neutral-700">
      <thead>
        <tr class="text-bold text-green-500 font-bold">
          <td>Name</td>
          <td>Email</td>
          <td>Phone</td>
          <td>Address</td>
          <td>Country</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(record, index) in this.records" v-bind:key="index">
          <td>{{ record.name }}</td>
          <td>{{ record.email }}</td>
          <td>{{ record.phone }}</td>
          <td>{{ record.address }}</td>
          <td>{{ record.country }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: 'TableComponent',
  props: {
    records: {
      type: Array
    }
  },
  // lifecycle hooks of events as given here https://v3.vuejs.org/api/options-lifecycle-hooks.html
  mounted() {},
  // end lifecycle hooks
  components: {},
  data() {
    return {
      data1: ''
    }
  },
  computed: {},
  methods: {
    method1() {}
  }
}
</script>
