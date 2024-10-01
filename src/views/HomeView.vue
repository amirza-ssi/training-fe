<template>
  <dropdown-component
    :title="this.dropdown_title"
    :options="this.dropdown_options"
    @dropdown-response="getDropdownInput"
  ></dropdown-component>
</template>
<script>
import DropdownComponent from '../components/DropdownComponent.vue'

export default {
  name: 'HomeView',
  props: {},
  mounted() {},
  components: { DropdownComponent },
  data() {
    const options = [
      { id: 1, title: 'Ruby on Rails' },
      { id: 2, title: 'Vue.js' },
      { id: 3, title: 'Tailwind CSS' },
      { id: 4, title: 'Node JS' }
    ]

    return {
      dropdown_title: 'Dropdown Title Test',
      dropdown_options: options
    }
  },
  computed: {},
  methods: {
    getDropdownInput(key) {
      console.log('The value of the key defined is:', key)
    },
    method2() {},
    method3() {}
  }
}
</script>
