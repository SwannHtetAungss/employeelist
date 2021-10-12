<template>
  <div>
    <h2>Employees List</h2>
    <!-- <table class="table responsive">
			<thead>
				<tr>
					<th>No.</th>
					<th>Name</th>
					<th>Photo</th>
					<th>Email</th>
					<th>Phone</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="employee in employees" :key="employee">
					<td>1</td>
					<td>{{employee.name}}</td>
					<td><img :src="employee.photo"></td>
					<td>{{employee.email}}</td>
					<td>{{employee.phone_number}}</td>
				</tr>
			</tbody>
		</table> -->
    <b-table-simple hover small caption-top responsive>
      <caption>
        Employee data in Our Company
      </caption>
      <b-thead head-variant="dark">
        <b-tr>
          <b-th>No.</b-th>
          <b-th>Photo</b-th>
          <b-th>Name</b-th>
          <b-th>Email</b-th>
          <b-th>Phone Number</b-th>
        </b-tr>
      </b-thead>
      <b-tbody>
        <b-tr v-for="(employee, index) in employees.data" :key="employee.id">
          <b-td>{{ ++index }}</b-td>
          <b-td
            ><img
              :src="employee.photo"
              alt="Photo"
              style="width: 80px;height:80px"
          /></b-td>
          <b-td>{{ employee.name }}</b-td>
          <b-td>{{ employee.email }}</b-td>
          <b-td>{{ employee.phone_number }}</b-td>
        </b-tr>
      </b-tbody>
    </b-table-simple>
    <pagination :data="employees" @pagination-change-page="getEmployees"
      ><span slot="prev-nav">&lt; Previous</span>
      <span slot="next-nav">Next &gt;</span></pagination
    >
  </div>
</template>

<script type="text/javascript">
const axios = require("axios");
export default {
  data() {
    return {
      employees: [],
    };
  },
  mounted() {
    this.getEmployees();
  },
  methods: {
    getEmployees(page = 1) {
      axios
        .get("http://localhost:8000/api/getemployee?page=" + page)
        .then((res) => {
          this.employees = res.data;
        });
    },
  },
};
</script>

<style type="text/css"></style>
