<template>
  <div v-if="isVisible">
    <div class="fixed inset-0 z-20 flex justify-center items-center text-slate-950">
      <div class="flex flex-col max-w-5xl rounded-lg shadow-lg bg-white border-cyan-300">
        <!-- Modal Header -->
        <div class="p-5">
          <div class="flex justify-between items-start">
            <h3 class="text-2xl font-semibold">Modal Header</h3>
            <button class="p-1 leading-none">
              <div class="text-xl font-semibold h-6 w-6" @click="cancelModal">
                <span> x</span>
              </div>
            </button>
          </div>
        </div>
        <!-- Modal Body -->
        <div class="p-6">
          <p>{{ JSON.stringify(formData) }}</p>
          <form>
            <input
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
            />
          </form>

          <dropdown-component
            title="Country "
            :options="this.country_options"
            @dropdown-response="(val) => (formData.country = val)"
          ></dropdown-component>
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
      { id: 1, title: 'Ruby on Rails' },
      { id: 2, title: 'Vue.js' },
      { id: 3, title: 'Tailwind CSS' },
      { id: 4, title: 'Node JS' }
    ]

    return {
      isVisible: false,
      formData: { name: '', email: '', phone: '', address: '', country: '' },
      country_options: options
    }
  },
  computed: {},
  methods: {
    open() {
      this.isVisible = true
    },
    cancelModal() {
      this.isVisible = false
    },
    confirmModal() {
      this.isVisible = false
    }
  }
}
</script>
