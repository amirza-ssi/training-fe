<template>
  <DropdownComponent
    :title="this.dropdownTitle"
    :options="this.dropdownOptions"
    confirm="getDropdownInput"
  ></DropdownComponent>
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
  methods: {}
}
</script>
