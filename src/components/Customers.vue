<template>
  <div class="customers container">
    <Alert v-if="alert" :message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
    <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item of filterBy(customers,filterInput)">
          <td>{{ item.name }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.emali }}</td>
          <td><router-link :to="'/customer/'+item.id" class="btn btn-default">详情</router-link></button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from "./alert";
export default {
  name: "customers",
  data() {
    return {
      customers: [],
      alert: "",
      filterInput:""
    };
  },
  methods:{
    //筛选
    filterBy(customers,value){
      return customers.filter(val=>{
        //match方法检索指定值，并返回匹配结果的数组（对象）
        return val.name.match(value)||val.phone.match(value)||val.emali.match(value)
      })
    }
  },
  mounted() {
    this.axios.get("http://localhost:3000/users").then(response => {
      // console.log(response);
      this.customers = response.data;
    });
  },
  created() {
    // console.log(this.$route);
    if (this.$route.query.alert) {
      this.alert = this.$route.query.alert;
    }
  },
  components: {
    Alert
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
