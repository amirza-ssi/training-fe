<template>
  <tr class="text-left">
    <th class="p-3 font-extrabold text-green-600" v-for="col in formatColName" :key="col">
      {{ col.val }}
    </th>
  </tr>

  <tr v-for="record in data" :key="record.id">
    <td v-for="(col, i) in cols" :key="i">{{ col != "image" ? record[col] : "<img src='"+ record[col] +"' / >" }}</td>
  </tr>
</template>

<script>
export default {
  name: 'DataTable',
  props: {
    data: {
      type: Array
    },
    cols: {
      type: Array
    }
  },
  // lifecycle hooks of events as given here https://v3.vuejs.org/api/options-lifecycle-hooks.html
  mounted() {},

  created() {},
  // end lifecycle hooks
  components: {},
  data() {
    return {
      rows: []
    }
  },
  computed: {
    formatColName() {
      //   console.log(this.cols.values().map((colName) => colName.upper()))
      return this.cols.map((c) => {
        return {
          // capitalize
          key: c,
          val: c
            .split('_')
            .map((c) => c.charAt(0).toUpperCase() + c.slice(1))
            .reduce((str, c) => str + ' ' + c, '').trim(),
        }
      })
    }
  },
  methods: {
    mapColumnKeysFromData() {
      var colSet = new Set([])
      this.data.forEach((row) => (colSet = new Set([...colSet, ...new Set(Object.keys(row))])))
      //   this.cols = colSet

      console.log(this.cols)
    }
  }
}
</script>
