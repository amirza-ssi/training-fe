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

<script setup>
import { orderBy } from 'lodash'
import { computed, onMounted, reactive, watch } from 'vue'
const props = defineProps({ data: Array, cols: Array })

onMounted(() => {
  rows.value = props.data
})

var rows = reactive([])
var isAscendingSorting = reactive({ a: 'a' })

watch(props, (p2, p1) => {
  rows.value = p2.data
})

// map column names automatically on state change
const formatColName = computed(() => {
  if (props.cols === undefined) return []
  return props.cols.map((c) => {
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
})

//sort data automatically on data or sorting change
const sortData = computed(() => {
  return orderBy(
    rows.value,
    Object.keys(isAscendingSorting.value || {}),
    Object.values(isAscendingSorting.value || {}).map((e) => (e === 1 ? 'asc' : 'desc'))
  )
})

function handleSort(column) {
  if (!isAscendingSorting.value || !isAscendingSorting.value[column.key]) {
    isAscendingSorting.value = {}
    isAscendingSorting.value[column.key] = 1
  }
  //if value exists already then set to descending
  else if (isAscendingSorting.value[column.key] === 1) {
    isAscendingSorting.value[column.key] = 0
  } else if (isAscendingSorting.value[column.key] === 0) {
    isAscendingSorting.value[column.key] = 1
  }
}
</script>
