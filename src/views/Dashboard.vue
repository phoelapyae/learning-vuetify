<template>
    <v-container>
        <h1>Dashboard</h1>

        <v-row>
          <v-col v-for="sale in sales" :key="`${sale.title}`" cols="12" md="4">
            <SalesGraph :sale="sale"/>
          </v-col>
        </v-row>

        <v-row>
          <v-col v-for="statistic in statistics" :key="`${statistic.title}`" cols="12" md="6" lg="3">
            <StatisticCard :statistic="statistic"/>
          </v-col>
        </v-row>
        
        <v-row>
          <v-col cols="12" md="8">
            <EmployeesTable :employees="employees" @select-employee="setEmployee"/>
          </v-col>
          <v-col cols="12" md="4">
            <EventTimeline :timeline="timeline"/>
          </v-col>
        </v-row>

        <!-- Snackbar  -->
        <v-snackbar
            v-model="snackbar"
            :left="$vuetify.breakpoint.lgAndUp"
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
    </v-container>
</template>

<script>

// component imports
import EmployeesTable from '../components/EmployeesTable'
import EventTimeline from '../components/EventTimeline'
import SalesGraph from '../components/SalesGraph'
import StatisticCard from '../components/StatisticCard'

// data imports
import employeesData from '../data/employees.json'
import timelineData from '../data/timeline.json'
import salesData from '../data/sales.json'
import statisticsData from '../data/statistics.json'

export default {
  components: {
    EmployeesTable,
    EventTimeline,
    SalesGraph,
    StatisticCard
  },
  data () {
    return {
      snackbar: false,
      selectedEmployee: {
        name: '',
        title: ''
      },
      employees: employeesData,
      sales: salesData,
      statistics: statisticsData,
      timeline: timelineData
    }
  },
  methods: {
    setEmployee(event){
      this.snackbar = true
      this.selectedEmployee.name = event.name
      this.selectedEmployee.title = event.title
    }
  }
}

</script>

<style scoped>

</style>