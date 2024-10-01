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
import { toRaw } from 'vue'
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
      this.$refs.modalComponent.open()
    },
    addUserDetails(user) {
      let userObj = toRaw(user)
      this.userData.push(userObj)
      console.log(this.userData)
      // console.log(userObj)
      // console.log(toRaw(user))
    }
  }
}
</script>
