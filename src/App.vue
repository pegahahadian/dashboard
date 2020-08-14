<template>
  <div id="app" class="small-container">
    <img src="./assets/logo.png" alt="vue logo">
    <h1>Form</h1>
    <employeeform @add:employee="addEmployee" />
    <hr>
    <h1>Employee List</h1>
        <employee-table :employees="employees" @delete:employee="deleteEmployee" @edit:employee="editEmployee"/>

  </div>
</template>

<script>
import employeeform from './components/employeeform.vue';
import EmployeeTable from '@/components/EmployeeTable.vue'

export default {
  name: 'app',
  components: {
    employeeform,
    EmployeeTable
  },
  methods: {
 addEmployee(employee) {
  const lastId =
    this.employees.length > 0
      ? this.employees[this.employees.length - 1].id
      : 0;
  const id = lastId + 1;
  const newEmployee = { ...employee, id };
  this.employees = [...this.employees, newEmployee];
},
  deleteEmployee(id) {
    this.employees = this.employees.filter(
      employee => employee.id !== id
    )
  },
  editEmployee(id, updatedEmployee) {
  this.employees = this.employees.map(employee =>
    employee.id === id ? updatedEmployee : employee
  )
},
editMode(employee) {
  this.cachedEmployee = Object.assign({}, employee)
  this.editing = employee.id
},
cancelEdit(employee) {
  Object.assign(employee, this.cachedEmployee)
  this.editing = null;
}

},
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Pegah Ahadian',
          email: 'p.a@yahoo.com',
        },
        {
          id: 2,
          name: 'Test Test',
          email: 'test@t.com',
        },
        {
          id: 3,
          name: 'Test2 Test2',
          email: 'test2@t2.com',
        },
      ],
    }
  },
}

</script>
<style>
#app {
  text-align: center;
  margin-top: 50px;
  color: rgb(71, 71, 71);
}
  button {
    background: #009435;
    border: 1px solid #009435;
    margin-top: 15px;
  }
  .small-container {
    max-width: 680px;
  }
</style>
