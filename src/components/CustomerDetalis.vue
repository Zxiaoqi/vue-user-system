<template>
  <div class="detalis container">
    <router-link class="btn btn-default" to="/">返回</router-link>
    <h1 class="page-header">
      {{ customer.name }}

      <span class="pull-right">
        <router-link class="btn btn-primary" :to="'/edit/' + customer.id"
          >编辑</router-link
        >
        <button class="btn btn-danger" @click="deleteCustomer(customer.id)">
          删除
        </button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item">
        <span class="glyphicon glyphicon-phone-alt"
          >&nbsp;{{ customer.phone }}</span
        >
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-envelope"
          >&nbsp;{{ customer.emali }}</span
        >
      </li>
    </ul>
    <ul class="list-group">
      <li class="list-group-item">
        <span class="glyphicon glyphicon-education"
          >&nbsp;{{ customer.education }}</span
        >
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-tower"
          >&nbsp;{{ customer.graduationschool }}</span
        >
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-th-large"
          >&nbsp;{{ customer.profession }}</span
        >
      </li>
      <li class="list-group-item">
        <span class="glyphicon glyphicon-user"
          >&nbsp;{{ customer.profile }}</span
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "customerdetalis",
  data() {
    return {
      customer: {}
    };
  },
  methods: {
    fetchCustomers(id) {
      this.axios.get("http://localhost:3000/users/" + id).then(response => {
        // console.log(response.data);
        this.customer = response.data;
      });
    },
    deleteCustomer(id) {
      this.axios.delete("http://localhost:3000/users/" + id).then(response => {
        this.$router.push({ path: "/", query: { alert: "用户删除成功！" } });
      });
    }
  },
  created() {
    this.fetchCustomers(this.$route.params.id);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
