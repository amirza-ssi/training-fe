<template>
  <!-- <div
    class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center"
    @click="handleButtonClick()"
  >
    <button>
      {{ title }}
    </button>
  </div> -->

  <!-- <div class="bg-white rounded min-w-40" v-show="isOptionVisible">
    <a
      href="#"
      class="block px-4 py-1 text-black"
      v-for="option in options"
      v-bind:key="option.id"
      v-on:click="handleOptionClick(option.id)"
      >{{ option.title }}</a
    >
  </div> -->
  <label>{{ title }}</label>
  <select
    class="block h-8 w-40 rounded overflow-hidden bg-green-500 text-center"
    v-model="selected"
    @change="handleOptionClick(selected)"
  >
    <option class="bg-white text-gray-700x" disabled value="">Please select one</option>
    <option class="bg-white text-gray-700x" v-for="option in options" v-bind:key="option.id">
      {{ option.title }}
    </option>
  </select>
</template>

<script setup>
import { ref } from 'vue'

defineProps({ title: { type: String }, options: {} })
const emit = defineEmits(['confirm'])

var isOptionVisible = ref(false)
var selected = ref('')

function handleOptionClick(option) {
  emit('confirm', option)
  isOptionVisible.value = false
}
function handleButtonClick() {
  isOptionVisible.value = !this.isOptionVisible
}
</script>
