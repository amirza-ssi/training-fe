<template>
  <DropdownComponent
    :title="dropdownTitle"
    :options="options"
    @confirm="getDropdownInput"
  ></DropdownComponent>
</template>
<script setup>
import { ref } from 'vue'
import DropdownComponent from '../components/DropdownComponent.vue'

const options = [
  { id: 1, title: 'Ruby on Rails' },
  { id: 2, title: 'Vue.js' },
  { id: 3, title: 'Tailwind CSS' },
  { id: 4, title: 'Node JS' }
]

function getDropdownInput(r) {
  console.log(r)
  dropdownTitle.value = r
}
var dropdownTitle = ref('Dropdown Title Test')
</script>
