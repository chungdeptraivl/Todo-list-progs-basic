<template>
  <div>
    <b-button v-b-modal.modal-prevent-closing>Add</b-button>

    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Submit Your Name"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group label="Name">
          <b-form-input v-model="student.name"></b-form-input>
        </b-form-group>
        <b-form-group label="Age">
          <b-form-input v-model="student.age"></b-form-input>
        </b-form-group>
        <b-form-group label="Phone">
          <b-form-input v-model="student.phone"></b-form-input>
        </b-form-group>
        <b-form-group label="Address">
          <b-form-input v-model="student.address"></b-form-input>
        </b-form-group>
      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    edit: {
      type: Object,
      default: null,
    },
  },

  data() {
    return {
      student: {
        id: Math.floor(Math.random() * 1000),
        name: '',
        age: '',
        phone: '',
        address: '',
      },
      name: '',
      nameState: null,
      submittedNames: [],
    }
  },

  watch: {
    edit() {
      if (this.edit) {
        this.student = Object.assign({}, this.edit)
      } else {
        this.student = {}
      }
    },
  },

  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity()
      this.nameState = valid
      return valid
    },
    resetModal() {
      this.name = ''
      this.nameState = null
    },
    handleOk(bvModalEvent) {
      this.$emit('submit', this.student);

      // eslint-disable-next-line no-unused-expressions
      this.student = {
        id: Math.floor(Math.random() * 1000),
        name: '',
        age: '',
        phone: '',
        address: '',
      }
      // Prevent modal from closing
      bvModalEvent.preventDefault()
      // Trigger submit handler
      this.handleSubmit()
    },
    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return
      }
      // Push the name to submitted names
      this.submittedNames.push(this.name)
      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide('modal-prevent-closing')
      })
    },
  },
}
</script>
