<template>
  <div id="employee-table">
    <table>
      <thead>
        <tr>
          <th>Employee Name</th>
          <th>Employee Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
    <tr v-for="employee in employees" :key="employee.id">
  <td v-if="editing === employee.id">
    <input type="text" v-model="employee.name" />
  </td>
  <td v-else>{{employee.name}}</td>
  <td v-if="editing === employee.id">
    <input type="text" v-model="employee.email" />
  </td>
  <td v-else>{{employee.email}}</td>
  <td v-if="editing === employee.id">
    <button @click="editEmployee(employee)">Save</button>
    <button class="muted-button" @click="editing = null">Cancel</button>
  </td>
  <td v-else>
    <button @click="editMode(employee.id)">Edit</button>
    <button @click="$emit('delete:employee', employee.id)">Delete</button>
  </td>
</tr>
      </tbody>
    </table>
  </div>
</template>
<script>
  export default {
    name: 'employee-table',
      props: {
    employees: Array,
  },
  data() {
  return {
    editing: null,
  }
},
methods: {
  editMode(id) {
    this.editing = id
  },

  editEmployee(employee) {
    if (employee.name === '' || employee.email === '') return
    this.$emit('edit:employee', employee.id, employee)
    this.editing = null
  }
}
  }
</script>
<style scoped>
  button {
    margin: 0 0.5rem 0 0;
    background-color: rgba(32, 32, 204, 0.815);
  }
  td, th{
      text-align: center;
  }
</style>