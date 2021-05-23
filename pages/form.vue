<template>
 <div class="container">
    <h1 class="text-center m-3">Form validation</h1>
    <form class="p-5 shadow rounded m-5" @submit.prevent="submitFrom" autocomplete="off">

    <div class="form-group">
        <label for="email">Email</label>
        <input
              type="text"
              v-model="form.email"
              @blur="$v.form.email.$touch()"
              class="form-control"
              :class="{'is-invalid': $v.form.email.$error, 'is-valid': !$v.form.email.$invalid && form.email}"
              id="email"
              placeholder="Enter your email">

        <small
              id="email"
              class="form-text text-danger"
              v-if="$v.form.email.$error">the email filed is wrong</small>

      </div>

      <div class="form-group">
        <label for="name">Name</label>
        <input
              type="text"
              v-model="form.name"
              @blur="$v.form.name.$touch()"
              class="form-control"
              :class="{'is-invalid': $v.form.name.$error, 'is-valid': !$v.form.name.$invalid}"
              id="name"
              placeholder="Enter your name">

        <small
              id="name"
              class="form-text text-danger"
              v-if="$v.form.name.$error">the name filed is required</small>
      </div>

      <div class="form-group">
        <label for="age">Age</label>
        <input
              type="text"
              v-model="form.age"
              @blur="$v.form.age.$touch()"
              class="form-control"
              :class="{'is-invalid': $v.form.age.$error, 'is-valid': !$v.form.age.$invalid}"
              id="age"
              placeholder="Enter your age">

          <div v-if="$v.form.age.$error">
            <small id="age" class="form-text text-danger" v-if="!$v.form.age.required">the age must be required</small>
            <small id="age" class="form-text text-danger" v-else-if="!$v.form.age.integer">the age must be integer</small>
            <small id="age" class="form-text text-danger" v-else-if="!$v.form.age.between">the age must be between 15 and 100</small>
          </div>
      </div>

      <div class="form-check">
        <input type="checkbox" v-model="form.isCheck" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>

      <button type="submit" class="btn btn-primary btn-lg btn-block mt-3">Submit</button>
      <pre>{{form}}</pre>
  </form>
</div>
</template>

<script>
import { required, email, numeric, minValue, minLength, maxValue, between, integer } from 'vuelidate/lib/validators'
  export default {
    data() {
      return {
        form: {
          name: null,
          email: null,
          age: null,
          isCheck: false
        }
      }
    },
    computed: {},
    validations: {
      form: {
        name: {
          required,
        },
        age: {
          required,
          integer,
          between: between(15, 100),
        },
        email: {
          email,
        },
      },
    },
    methods: {
      submitFrom() {
        this.$v.form.$touch()
        if (!this.$v.form.$invalid) {
          console.log(this.form);
        }
        else {
          console.log("invalid");
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
.form-check .form-check-label{
  cursor: pointer;
}
</style>
