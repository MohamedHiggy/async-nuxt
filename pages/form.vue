<template>
 <div class="container">
    <h1 class="text-center m-3">Form validation</h1>
    <form class="p-5 shadow rounded m-5" @submit.prevent="submitFrom" autocomplete="off">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" v-model="form.name" class="form-control" id="name" placeholder="Enter your name">
        <small id="name" class="form-text text-danger" v-if="!nameIsValid">the name filed is required</small>
      </div>

      <div class="form-group">
        <label for="age">Age</label>
        <input type="text" v-model.number="form.age" class="form-control" id="age" placeholder="Enter your age">
        <small id="age" class="form-text text-danger" v-if="!ageIsValid">the age must be at least 12 and max 100</small>
      </div>

      <div class="form-check">
        <input type="checkbox" v-model="form.isCheck" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>

      <button type="submit" :disabled="!formsIsValid" class="btn btn-primary btn-lg btn-block mt-3">Submit</button>
      <pre>{{form}}</pre>
  </form>
</div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          name: null,
          age: null,
          isCheck: false
        }
      }
    },
    computed: {
      nameIsValid(){
        return !!this.form.name
      },
      ageIsValid(){
        return typeof this.form.age === "number" && this.form.age > 12 && this.form.age < 100;
      },
      formsIsValid() {
        return this.nameIsValid && this.ageIsValid;
      }
    },
    methods: {
      submitFrom() {
        if (this.formsIsValid) {
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
