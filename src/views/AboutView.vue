<template>
  <div>
    <div class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center m-6">
      <button @click="handleAddUserClick">Add User</button>
    </div>
    <table-component :records="this.userData"></table-component>
  </div>
  <modal-component ref="modalComponent" @modal-confirm="addUserDetails"></modal-component>
</template>

<script>
import ModalComponent from '../components/Exercise2/ModalComponent.vue'
import TableComponent from '../components/Exercise2/TableComponent.vue'
export default {
  name: 'AboutView',
  props: {},
  // lifecycle hooks of events as given here https://v3.vuejs.org/api/options-lifecycle-hooks.html
  mounted() {},
  // end lifecycle hooks
  components: { ModalComponent, TableComponent },
  data() {
    return {
      userData: []
    }
  },
  computed: {},
  methods: {
    handleAddUserClick() {
      console.log()
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
      this.$refs.modalComponent.open('Add User', formConfig)

      // <input
      //         class="block my-2 border-2 p-2 rounded-lg min-w-40"
      //         v-model="formData.name"
      //         placeholder="Name"
      //       />
    },
    addUserDetails(user) {
      let userObj = {}

      user.forEach((input) => {
        console.log(input)
        userObj[input.label.toLowerCase()] = input.value
      })
      this.userData.push(userObj)
      console.log(this.userData)
      // console.log(userObj)
      // console.log(toRaw(user))
    }
  }
}
</script>
