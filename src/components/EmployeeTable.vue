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
          <td>{{ employee.name }}</td>
          <td>{{ employee.email }}</td>
          <td>
            <button>Edit</button>
            <button>Delete</button>
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
  }
</script>
<style scoped>
  button {
    margin: 0 0.5rem 0 0;
    background-color: rgba(32, 32, 204, 0.815);
  }
</style>