<template>
  <div class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center m-6">
    <button @click="handleAddColumns">Add Columns</button>
  </div>
  <DataTable :data="data1.value" :cols="columnSelected"></DataTable>
  <ModalComponent ref="modalComponent" @confirm="onModalClose"></ModalComponent>
</template>

<script setup>
import DataTable from '@/components/Exercise3/DataTable.vue'
import ModalComponent from '@/components/Exercise2/ModalComponent.vue'
import { ref, reactive, onMounted, useTemplateRef, watch } from 'vue'

var data1 = reactive([])
var columnSelected = ref([
  'image',
  'name',
  'symbol',
  'current_price',
  'market_cap',
  'price_change_percentage_24h'
])
var columnsData = ref([])

watch(columnSelected, () => {
  localStorage.setItem('ex3_columns', JSON.stringify(columnSelected.value))
})

const modalComponent = useTemplateRef('modalComponent')

// lifecycle hooks of events as given here https://v3.vuejs.org/api/options-lifecycle-hooks.html
onMounted(() => {
  fetch(
    'https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false'
  )
    .then((res) => res.json())
    //   .then((data) =>
    //map data to columns
    .then((data) => {
      data1.value = data
    })
    .then(() => {
      initColumnKeysFromData()
      loadStoredColumns()
    })
})

function initColumnKeysFromData() {
  var colSet = new Set([])
  data1.value.forEach((row) => (colSet = new Set([...colSet, ...new Set(Object.keys(row))])))
  columnsData.value = Array.from(colSet)
}
function loadStoredColumns() {
  let storedColumns = JSON.parse(localStorage.getItem('ex3_columns'))
  if (storedColumns !== null) {
    columnSelected.value = storedColumns
  }
}

function handleAddColumns() {
  //
  let formObj = [
    {
      input: 'checkbox',
      label: 'Select All',
      options: columnsData.value,
      value: columnSelected.value
    }
  ]

  modalComponent.value.open('Add Column', formObj)
}

function onModalClose(formObj) {
  columnSelected.value = formObj[0].value
}
</script>
