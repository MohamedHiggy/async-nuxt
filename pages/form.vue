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
              :class="{'is-invalid': shouldAppendErroClass($v.form.email), 'is-valid': shouldAppendValidClass($v.form.email)}"
              id="email"
              placeholder="Enter your email">

          <small
              id="email"
              class="form-text text-danger"
              v-if="!$v.form.email.required && $v.form.email.$error">the email filed is required
          </small>
          <small
              id="email"
              class="form-text text-danger"
              v-else-if="!$v.form.email.email && $v.form.email.$error">the email filed is wrong
          </small>

      </div>

      <div class="form-group">
        <label for="name">Name</label>
        <input
              type="text"
              v-model="form.name"
              @blur="$v.form.name.$touch()"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.name), 'is-valid': shouldAppendValidClass($v.form.name)}"
              id="name"
              placeholder="Enter your name">

        <small
              id="name"
              class="form-text text-danger"
              v-if="$v.form.name.$error">the name filed is required</small>
      </div>

      <div class="form-group">
        <label for="food">Pizza or Burger</label>
        <input
              type="text"
              v-model="form.food"
              @blur="$v.form.food.$touch()"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.food), 'is-valid': shouldAppendValidClass($v.form.food)}"
              id="food"
              placeholder="Enter your food">

        <small
              id="food"
              class="form-text text-danger"
              v-if="$v.form.food.$error && !$v.form.food.pizzaOrBurger">Sorry! We only serve pizzas and burgers </small>
      </div>

      <div class="form-group">
        <label for="age">Age</label>
        <input
              type="text"
              v-model="form.age"
              @blur="$v.form.age.$touch()"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.age), 'is-valid': shouldAppendValidClass($v.form.age)}"
              id="age"
              placeholder="Enter your age">

          <div v-if="$v.form.age.$error">
            <small id="age" class="form-text text-danger" v-if="!$v.form.age.required">the age must be required</small>
            <small id="age" class="form-text text-danger" v-else-if="!$v.form.age.integer">the age must be integer</small>
            <small id="age" class="form-text text-danger" v-else-if="!$v.form.age.between">the age must be between 15 and 100</small>
          </div>
      </div>

      <div class="form-group" style="position:relative">
        <label for="github-username">Github username</label>
        <input
              type="text"
              v-model.lazy="$v.form.githubUsername.$model"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.githubUsername), 'is-valid': shouldAppendValidClass($v.form.githubUsername)}"
              id="github-username"
              placeholder="Your github username">

            <div v-show="$v.form.githubUsername.$pending" class="spinner-grow" style="width: 1rem; height: 1rem;position:absolute; bottom:35px; right:15px" role="status">
              <span class="sr-only">Loading...</span>
            </div>

            <small
              id="github-username"
              class="form-text text-danger"
              v-if="!$v.form.githubUsername.exists && $v.form.githubUsername">there is not github user with this username
            </small>
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input
              type="password"
              v-model="form.password"
              @blur="$v.form.password.$touch()"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.password), 'is-valid': shouldAppendValidClass($v.form.password)}"
              id="password"
              placeholder="Enter your password">
              <small
              id="password"
              class="form-text text-danger"
              v-if="!$v.form.password.required && $v.form.password.$error">the password filed is required
          </small>
          <small
              id="email"
              class="form-text text-danger"
              v-else-if="!$v.form.password.minLength && $v.form.password.$error">the password filed must be more than 6 letters
          </small>
          <small
              id="email"
              class="form-text text-danger"
              v-else-if="!$v.form.password.valid && $v.form.password.$error">
              password must be at least
              <ul>
                <li>contains Uppercase</li>
                <li>contains Lowercase</li>
                <li>contains Number</li>
                <li>contains Special</li>
              </ul>
          </small>
      </div>

      <div class="form-group">
        <label for="confirm-password">Confirm Password</label>
        <input
              type="password"
              v-model="form.repeatPassword"
              @blur="$v.form.repeatPassword.$touch()"
              class="form-control"
              :class="{'is-invalid': shouldAppendErroClass($v.form.repeatPassword), 'is-valid': shouldAppendValidClass($v.form.repeatPassword)}"
              id="confirm-password"
              placeholder="Enter your Confirm password">

              <small
              id="password"
              class="form-text text-danger"
              v-if="!$v.form.repeatPassword.sameAsPassword && $v.form.repeatPassword.$error">Passwords must be identical.
          </small>
      </div>

      <div class="form-check">
        <input type="checkbox" @change="$v.form.isCheck.$touch()" :class="{'is-invalid': shouldAppendErroClass($v.form.isCheck), 'is-valid': shouldAppendValidClass($v.form.isCheck)}" v-model="form.isCheck" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">agree anything</label>
        <small
              id="exampleCheck1"
              class="form-text text-danger"
              v-if="!$v.form.isCheck.sameAs && $v.form.isCheck.$error">must be check
          </small>
      </div>



      <button class="btn btn-primary btn-lg btn-block mt-3" v-if="isLoading" type="button" disabled>
        <span class="spinner-grow spinner-grow-sm" role="status" aria-hidden="true"></span>
        Loading...
      </button>
      <button type="submit" class="btn btn-primary btn-lg btn-block mt-3" v-else>Submit</button>
  </form>
</div>
</template>

<script>
import { required, email, sameAs, minLength, between, integer, helpers } from 'vuelidate/lib/validators'
import axios from "axios"
  export default {
    data() {
      return {
        form: {
          name: null,
          email: null,
          age: null,
          food: null,
          password: null,
          repeatPassword: null,
          githubUsername: null,
          isCheck: false
        },
        isLoading: false
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
          required,
          email,
        },
        food: {
          pizzaOrBurger: value => value === 'pizza' || value === 'burger' || !helpers.req(value),
        },
        githubUsername: {
          exists(value) {
            if (!helpers.req(value)) {
              return true
            }
            return axios.get(`https://api.github.com/users/${value}`)
          }
        },
        password: {
          required,
          minLength: minLength(6),
          valid: function(value) {
            const containsUppercase = /[A-Z]/.test(value)
            const containsLowercase = /[a-z]/.test(value)
            const containsNumber = /[0-9]/.test(value)
            const containsSpecial = /[#?!@$%^&*-]/.test(value)
            return containsUppercase && containsLowercase && containsNumber && containsSpecial
          }
        },
        repeatPassword: {
          sameAsPassword: sameAs('password')
        },
        isCheck:{
          sameAs: sameAs( () => true )
        }
      },
    },
    methods: {
      shouldAppendValidClass(target){
        return !target.$invalid && target.$model && target.$dirty
      },
      shouldAppendErroClass(target){
        return target.$error
      },
      submitFrom() {
        this.$v.form.$touch()

        if (!this.$v.form.$invalid) {
          this.isLoading = true
          setTimeout(() => {
            this.isLoading = false
            console.log(this.form)
          }, 1000);
        }
        else {
            console.log("invalid")
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
