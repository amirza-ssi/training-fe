<template>
  <div
    class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center"
    v-on:click="handleButtonClick()"
  >
    <button>
      {{ title }}
    </button>
  </div>

  <div class="bg-white rounded min-w-40" v-if="isOptionVisible">
    <a
      href="#"
      class="block px-4 py-1 text-black"
      v-for="option in options"
      v-bind:key="option.id"
      v-on:click="handleOptionClick(option.id)"
      >{{ option.title }}</a
    >
  </div>
</template>
<script>
export default {
  name: 'DropdownComponent',
  props: { title: { type: String }, options: {} },
  mounted() {
    console.log(this.options)
  },
  components: {},
  data() {
    return {
      isOptionVisible: false
    }
  },
  emits: ['dropdown-response'],
  computed: {},
  methods: {
    handleOptionClick(option) {
      this.$emit('dropdown-response', option)
      this.isOptionVisible = false
    },
    handleButtonClick() {
      // console.log('Before change', this.options)
      this.isOptionVisible = !this.isOptionVisible
      // console.log('After change', this.isOptionVisible)
    },
    method3() {}
  }
}
</script>
