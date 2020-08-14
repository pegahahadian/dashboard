<template>
  <div id="employeeform">
    <form @submit.prevent="handleSubmit">
      <label>Name</label>
      <input ref="first"
    type="text"
    :class="{ 'has-error': submitting && invalidName }"
    v-model="employee.name"
    @focus="clearStatus"
    @keypress="clearStatus"/>
      <label> Email</label>
      <input type="text"
    :class="{ 'has-error': submitting && invalidEmail }"
    v-model="employee.email"
    @focus="clearStatus"/>
       <label>Password</label>
      <input type="password"
    :class="{ 'has-error': submitting && invalidPassword }"
    v-model="employee.password"
    @focus="clearStatus"/>
      <p v-if="error && submitting" class="error-message">
    ❗Please fill out all required fields
  </p>
  <p v-if="success" class="success-message">
    ✅ Employee successfully added
  </p>
      <button>Add Employee</button>
    </form>
  </div>
</template>
<script>

  export default {
    name: 'employeeform',
    methods: {
  handleSubmit() {
    this.submitting = true
    this.clearStatus()
    if (this.invalidName || this.invalidEmail) {
      this.error = true
      return
    }
    this.$emit('add:employee', this.employee)
    this.$refs.first.focus()
    this.employee = {
      name: '',
      email: '',
      password:'',
    }
    this.error = false
    this.success = true
    this.submitting = false
  },
  clearStatus() {
    this.success = false
    this.error = false
  }
    },
    data() {
    return {
         submitting: false,
    error: false,
    success: false,
    employee: {
      name: '',
      email: '',
      password:'',
    }
    }
  },
  computed: {
  invalidName() {
    return this.employee.name === ''
  },
  invalidEmail() {
    return this.employee.email === ''
  },
    invalidPassword() {
    return this.employee.password === ''
  },
},
  }
</script>
<style scoped>
  form {
    margin-bottom: 2rem;
    border: 2px solid rgba(20, 54, 126, 0.555);
    padding: 30px;
  }
  [class*='-message'] {
    font-weight: 500;
  }
  .error-message {
    color: #d33c40;
  }
  .success-message {
    color: #32a95d;
  }
</style>