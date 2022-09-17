<script>
import axios from 'axios'
import BaseInput from './components/BaseInput.vue'
import BaseSelect from './components/BaseSelect.vue'
export default {
  name: 'app',
  components: {
    BaseInput,
    BaseSelect
  },
  data() {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        telephone: '',
        love: ''
      },
      loveOptions: [
        { label: 'Fun to use', value: 'fun' },
        { label: 'Friendly learning curve', value: 'curve' },
        { label: 'Amazing documentation', value: 'docs' },
        { label: 'Fantastic community', value: 'community' }
      ]
    }
  },
  methods: {
    onSubmit() {
      if (this.validForm === true) {
        axios.post('http://localhost:2525/form', this.form)
          .then(res => {
            console.log('Form has been posted', res)
          }).catch(err => {
            console.log('An error occured', err)
          })
      } else {
        console.log('click')
        return
      }
      this.form.firstName = ''
      this.form.lastName = ''
      this.form.email = ''
      this.form.telephone = ''
    }
  },
  computed: {
    validForm() {
      if (this.form.firstName != '' && this.form.lastName != '' && this.form.email != '') {
        return true
      } else {
        return false
      }
    }
  }
}
</script>

<template>
  <div class="app">
    <div class="row">
      <div class="col-12">
        <form @submit.prevent="onSubmit">
          <div class="form-group">
            <BaseInput label="First Name" v-model="form.firstName" type="text" />
          </div>
          <div class="form-group">
            <BaseInput label="Last Name" v-model="form.lastName" type="text" />
          </div>
          <div class="form-group">
            <BaseInput label="Email" v-model="form.email" type="email" />
          </div>
          <div class="form-group">
            <BaseInput label="Telephone Number" v-model="form.telephone" type="text" :mask="'(###)###-####'" />
          </div>
          <BaseSelect label="Vue is fun" :options="loveOptions" v-model="form.love" />
          <br>
          <div class="form-group">
            <button class="btn btn-primary" type="submit" @click.prevent="onSubmit"
              :disabled="!this.validForm">Submit</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
