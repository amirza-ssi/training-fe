<template>
  <dropdown-component
    :title="this.dropdownTitle"
    :options="this.dropdownOptions"
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
      dropdownTitle: 'Dropdown Title Test',
      dropdownOptions: options
    }
  },
  computed: {},
  methods: {
    getDropdownInput(key) {},
    method2() {},
    method3() {}
  }
}
</script>
