<template>
  <div v-if="isVisible">
    <div
      class="my-5 py-5 fixed inset-0 z-20 flex justify-center items-center overflow-auto text-slate-950"
    >
      <div class="flex flex-col max-w-5xl min-w-96 rounded-lg shadow-lg bg-white border-cyan-300">
        <!-- Modal Header -->
        <div class="p-5">
          <div class="flex justify-between items-start">
            <h3 class="text-2xl font-semibold">{{ headerText }}</h3>
            <button class="p-1 leading-none">
              <div class="text-xl font-semibold h-6 w-6" @click="cancelModal">
                <span> x</span>
              </div>
            </button>
          </div>
        </div>
        <!-- Modal Body -->
        <div class="p-6">
          <form>
            <div v-for="(field, i) in bodyForm.value" v-bind:key="i">
              <input
                v-if="field.input === 'text'"
                type="text"
                :placeholder="field.label"
                v-model="field.value"
                class="block my-2 border-2 p-2 rounded-lg"
              />

              <div v-if="field.input === 'checkbox'">
                <p>{{ field.label }}</p>
                <div class="grid grid-cols-2 py-2">
                  <div v-for="option in field.options" v-bind:key="option" class="mr-5 mb-2">
                    <!-- @change="handleCheckboxChange(option, field)" -->

                    <label class="ml-1">
                      <input
                        type="checkbox"
                        :id="option.key"
                        :value="option"
                        v-model="option.selected"
                        class="m-2"
                      />{{ formatColName(option.key) }}
                    </label>
                  </div>
                </div>
              </div>

              <div v-if="field.input === 'dropdown'">
                <DropdownComponent
                  title="Country "
                  :options="field.options"
                  @confirm="(r) => handleDropdownResponse(r, field)"
                >
                  {{ field.label }}
                </DropdownComponent>
              </div>
            </div>
          </form>
        </div>

        <!-- Modal Footer -->
        <div class="p-6 flex justify-end items-center">
          <button
            class="block h-8 w-20 mx-6 rounded overflow-hidden bg-green-500 text-center px-4"
            @click="cancelModal"
          >
            Cancel
          </button>
          <button
            class="block h-8 w-20 mx-6 rounded overflow-hidden bg-green-500 text-center px-4"
            @click="confirmModal"
          >
            Confirm
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive } from 'vue'
import DropdownComponent from '../DropdownComponent.vue'

const options = [
  { id: 'PK', title: 'Pakistan' },
  { id: 'US', title: 'United States' },
  { id: 'UK', title: 'United Kingdom' },
  { id: 'CA', title: 'Canada' }
]

var isVisible = ref(false)
var headerText = ref('')
var formData = reactive({ name: '', email: '', phone: '', address: '', country: '' })
var bodyForm = reactive([])
const emit = defineEmits(['confirm'])

// map column names automatically on state change
function formatColName(c) {
  return c
    .split('_')
    .map((c) => c.charAt(0).toUpperCase() + c.slice(1))
    .reduce((str, c) => str + ' ' + c, '')
    .trim()
}

function open(header, body) {
  headerText.value = header
  bodyForm.value = body

  isVisible.value = true

  bodyForm.value
    //for all checkbox items
    .filter((item) => item.input === 'checkbox')
    .forEach((checkboxItem) =>
      //map array into object
      {
        checkboxItem.options = checkboxItem.options.map((option) => {
          // {key: field_name , selected: boolean if in val }
          return { key: option, selected: checkboxItem.value.includes(option) }
        })
      }
    )
}
defineExpose({ open })
function cancelModal() {
  isVisible.value = false
}
function confirmModal() {
  reverseMapCheckboxData()

  emit('confirm', bodyForm.value)
  isVisible.value = false
  formData.value = createEmptyFormData()
}

function reverseMapCheckboxData() {
  bodyForm.value
    //for all checkbox items
    .filter((item) => item.input === 'checkbox')
    .forEach((checkboxItem) =>
      //map array into object
      {
        checkboxItem.value = checkboxItem.options
          .filter((o) => o.selected)
          .reduce((o1, o2) => o1.concat(o2.key), [])
        checkboxItem.options = checkboxItem.options.reduce((o1, o2) => o1.concat(o2.key), [])
      }
    )
}
function createEmptyFormData() {
  return { name: '', email: '', phone: '', address: '', country: '' }
}
function handleDropdownResponse(r, field) {
  field['value'] = r

  console.log('handeldropdownresponse end')
}
// handleCheckboxChange(option, field) {
//   //
//
//

//   if (field.value.includes(option)) {
//     field.value = field.value.filter((val) => val != option)
//   } else {
//     field.value.push(option)
//   }
// }
</script>
