<template>
  <tr class="text-left">
    <th
      class="p-1 font-extrabold text-green-600"
      v-for="(col, i) in formatColName"
      :key="col"
      @click="handleSort(col, i)"
    >
      {{ col.val }}
    </th>
  </tr>

  <tr v-for="record in sortData" :key="record.id">
    <!-- <td class="m-10" v-for="(col, i) in columns" :key="i">{{ col != "image" ? record[col] : "<img src='"+ record[col] +"' / ></img>" }}</td> -->
    <td class="m-10" v-for="(col, i) in columns" :key="i">{{ record[col] }}</td>
  </tr>
</template>

<script>
import { orderBy } from 'lodash'
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
      columns: [...this.cols],
      rows: this.data,
      isAscendingSorting: {}
    }
  },
  computed: {
    // map column names automatically on state change
    formatColName() {
      console.log(this.columns)
      return this.columns.map((c) => {
        return {
          // capitalize
          key: c,
          val: c
            .split('_')
            .map((c) => c.charAt(0).toUpperCase() + c.slice(1))
            .reduce((str, c) => str + ' ' + c, '')
            .trim()
        }
      })
    },

    //sort data automatically on data or sorting change
    sortData() {
      return orderBy(
        this.rows,
        Object.keys(this.isAscendingSorting),
        Object.values(this.isAscendingSorting).map((e) => (e === 1 ? 'asc' : 'desc'))
      )

      // return this.rows
    }
  },
  methods: {
    // sort on click of any column heading
    handleSort(column, index) {
      console.log(column.key)
      console.log(this.isAscendingSorting[column.key] === 1)
      //if valuobjecte exists already then set to descending
      if (this.isAscendingSorting[column.key] === 1) {
        this.isAscendingSorting[column.key] = 0
      } else {
        this.isAscendingSorting[column.key] = 1
      }
      // default add value as ascending

      console.log(JSON.stringify(this.isAscendingSorting))
    }
  }
}
</script>
