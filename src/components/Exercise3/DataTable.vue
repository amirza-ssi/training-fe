<template>
  <tr class="text-left">
    <th
      class="p-2 font-extrabold text-green-600"
      v-for="(col, i) in formatColName"
      :key="col"
      @click="handleSort(col, i)"
    >
      {{ col.val }}
    </th>
  </tr>

  <tr v-for="record in sortData" :key="record.id">
    <!-- <td class="m-10" v-for="(col, i) in columns" :key="i">{{ col != "image" ? record[col] : "<img src='"+ record[col] +"' / ></img>" }}</td> -->
    <td class="p-2 align-middle" v-for="(col, i) in cols" :key="i">
      <img class="max-h-12" v-if="col === 'image'" :src="record[col]" />
      <p v-else>{{ record[col] }}</p>
    </td>
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
      rows: this.data,
      isAscendingSorting: {}
    }
  },
  watch: {
    data() {
      console.log(this.data)
    }
  },
  computed: {
    // map column names automatically on state change
    formatColName() {
      if (this.cols === undefined) return []
      return this.cols.map((c) => {
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
    handleSort(column) {
      //if value exists already then set to descending
      if (this.isAscendingSorting[column.key] === 1) {
        this.isAscendingSorting[column.key] = 0
      } else {
        this.isAscendingSorting[column.key] = 1
      }
      // default add value as ascending
    }
  }
}
</script>
