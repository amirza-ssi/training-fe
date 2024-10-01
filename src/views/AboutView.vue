<template>
  <div class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center">
    <button @click="handleAddUserClick">Add User</button>
  </div>
  <modal-component ref="modalComponent" @modal-confirm="addUserDetails"></modal-component>
  <div>
    <table-component></table-component>
  </div>
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
      data1: ''
    }
  },
  computed: {},
  methods: {
    handleAddUserClick() {
      console.log()
      this.$refs.modalComponent.open()
    },
    addUserDetails(user) {
      console.log(user)
    }
  }
}
</script>
