<template>
  <div v-if="isVisible">
    <div class="fixed inset-0 z-20 flex justify-center items-center text-slate-950">
      <div class="flex flex-col max-w-5xl min-w-96 rounded-lg shadow-lg bg-white border-cyan-300">
        <!-- Modal Header -->
        <div class="p-5">
          <div class="flex justify-between items-start">
            <h3 class="text-2xl font-semibold">{{ this.headerText }}</h3>
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
            <div v-for="(field, i) in bodyForm" v-bind:key="i">
              <input
                v-if="field.input === 'text'"
                type="text"
                :placeholder="field.label"
                v-model="field.value"
                class="block my-2 border-2 p-2 rounded-lg"
              />

              <div v-if="field.input === 'checkbox'">
                <p>{{ field.label }}</p>
                <div v-for="option in field.options" v-bind:key="option" class="inline-block mr-5">
                  <input type="checkbox" id="checkbox" :value="option" v-model="option.selected" />
                  <!-- @change="handleCheckboxChange(option, field)" -->

                  <label class="ml-1" for="checkbox">{{ option.key }}</label>
                </div>
              </div>
            </div>

            <!-- <input
              class="block my-2 border-2 p-2 rounded-lg min-w-40"
              v-model="formData.name"
              placeholder="Name"
            />
            <input
              class="block my-2 border-2 p-2 rounded-lg min-w-40"
              v-model="formData.email"
              placeholder="Email"
            />
            <input
              class="block my-2 border-2 p-2 rounded-lg min-w-40"
              v-model="formData.phone"
              placeholder="Phone"
            />
            <input
              class="block my-2 border-2 p-2 rounded-lg min-w-40"
              v-model="formData.address"
              placeholder="Address"
            /> -->
          </form>

          <dropdown-component
            title="Country "
            :options="this.country_options"
            @dropdown-response="(val) => (formData.country = val)"
          ></dropdown-component>
          <span>{{ formData.country }}</span>
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
<script>
import DropdownComponent from '../DropdownComponent.vue'
export default {
  name: 'ModalComponent',
  props: {},
  // lifecycle hooks of events as given here https://v3.vuejs.org/api/options-lifecycle-hooks.html
  mounted() {},
  // end lifecycle hooks
  components: { DropdownComponent },
  data() {
    const options = [
      { id: 'PK', title: 'Pakistan' },
      { id: 'US', title: 'United States' },
      { id: 'UK', title: 'United Kingdom' },
      { id: 'CA', title: 'Canada' }
    ]

    return {
      isVisible: false,
      headerText: '',
      formData: { name: '', email: '', phone: '', address: '', country: '' },
      country_options: options,
      bodyForm: []
    }
  },
  computed: {},
  methods: {
    open(header, bodyForm) {
      this.headerText = header
      this.bodyForm = bodyForm
      console.log('On modal init: ', this.bodyForm[0])

      this.isVisible = true

      this.bodyForm
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
    },
    cancelModal() {
      this.isVisible = false
    },
    confirmModal() {
      this.reverseMapCheckboxData()

      this.$emit('modal-confirm', this.bodyForm)
      this.isVisible = false
      this.formData = this.createEmptyFormData()

      console.log('On Modal Close: ', this.bodyForm)
    },
    reverseMapCheckboxData() {
      this.bodyForm
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
    },
    createEmptyFormData() {
      return { name: '', email: '', phone: '', address: '', country: '' }
    }
    // handleCheckboxChange(option, field) {
    //   // console.log(option, field)
    //   console.log(field.value)
    //   console.log(field.value.includes(option))

    //   if (field.value.includes(option)) {
    //     field.value = field.value.filter((val) => val != option)
    //   } else {
    //     field.value.push(option)
    //   }
    // }
  }
}
</script>
