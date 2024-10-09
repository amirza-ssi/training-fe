<template>
  <div>
    <div class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center m-6">
      <button @click="handleAddUserClick">Add User</button>
    </div>
    <DataTable :data="userData" :cols="dataColumns"></DataTable>
  </div>
  <ModalComponent ref="modalComponent" @confirm="addUserDetails"></ModalComponent>
</template>

<script setup>
import ModalComponent from '@/components/Exercise2/ModalComponent.vue'
import DataTable from '@/components/Exercise3/DataTable.vue'
import { ref, useTemplateRef } from 'vue'

var userData = ref([])
var dataColumns = ref(['name', 'email', 'phone', 'address', 'country'])
const modalComponent = useTemplateRef('modalComponent')

function handleAddUserClick() {
  let formConfig = [
    { input: 'text', label: 'Name', value: '' },
    { input: 'text', label: 'Email', value: '' },
    { input: 'text', label: 'Phone', value: '' },
    { input: 'text', label: 'Address', value: '' },
    {
      input: 'dropdown',
      label: 'Country',
      value: '',
      options: [
        { id: 'PK', title: 'Pakistan' },
        { id: 'US', title: 'United States' },
        { id: 'UK', title: 'United Kingdom' },
        { id: 'CA', title: 'Canada' }
      ]
    }
  ]
  modalComponent.value.open('Add User', formConfig)
}
function addUserDetails(user) {
  let userObj = {}

  user.forEach((input) => {
    userObj[input.label.toLowerCase()] = input.value
  })
  userData.value.push(userObj)
}
</script>
