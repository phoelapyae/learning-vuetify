<template>
    <div>
        <h1>Dashboard</h1>
        <v-data-table
            @click:row="selectRow"
            :headers="headers"
            :items="employees"
            :items-per-page="5"
            class="elevation-1"
            multi-sort
        ></v-data-table>

        <!-- Snackbar  -->
        <v-snackbar
            v-model="snackbar"
        >
            Your selected name is {{ selectedEmployee.name }} and selected title is {{ selectedEmployee.title }}.
            <v-btn
                color="pink"
                text
                @click="snackbar = false"
            >
                Close
            </v-btn>
        </v-snackbar>

    </div>
</template>

<script>
import Employees from '../data/employees.json';
  export default {
    data () {
      return {
        snackbar: false,
        currentItem: '',
        selectedEmployee: {
          name: '',
          title: ''
        },
        headers: [
          { text: 'Employee ID', value: 'id' },
          { text: 'Name', value: 'name' },
          { text: 'Title', value: 'title' },
          { text: 'Salary', value: 'salary' }
        ],
        employees: Employees
      }
    },
    methods: {
        selectRow(event){
            this.snackbar = true
            this.selectedEmployee.name = event.name
            this.selectedEmployee.title = event.title
        }
    }
  }
</script>

<style scoped>

</style>