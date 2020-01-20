<template>
  <div class="edit container">
    <Alert v-if="alert" :message="alert"></Alert>
    <h1 class="page-header">编辑用户</h1>
    <form @submit.prevent="updataCustomer()">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label>姓名</label>
          <input
            type="text"
            class="form-control"
            placeholder="name"
            v-model="customer.name"
          />
        </div>
        <div class="form-group">
          <label>电话</label>
          <input
            type="text"
            class="form-control"
            placeholder="phone"
            v-model="customer.phone"
          />
        </div>
        <div class="form-group">
          <label>邮箱</label>
          <input
            type="text"
            class="form-control"
            placeholder="emali"
            v-model="customer.emali"
          />
        </div>
        <div class="form-group">
          <label>学历</label>
          <input
            type="text"
            class="form-control"
            placeholder="education"
            v-model="customer.education"
          />
        </div>
        <div class="form-group">
          <label>毕业学校</label>
          <input
            type="text"
            class="form-control"
            placeholder="graduationschool"
            v-model="customer.graduationschool"
          />
        </div>
        <div class="form-group">
          <label>职业</label>
          <input
            type="text"
            class="form-control"
            placeholder="profession"
            v-model="customer.profession"
          />
        </div>
        <div class="form-group">
          <label>个人简介</label>
          <textarea
            class="form-control"
            rows="10"
            v-model="customer.profile"
          ></textarea>
        </div>
        <button type="submit" class="btn btn-primary">确认</button>
      </div>
    </form>
  </div>
</template>

<script>
import Alert from "./alert";
export default {
  name: "add",
  data() {
    return {
      customer: {},
      alert: ""
    };
  },
  methods: {
    fetchCustomer(id) {
      this.axios.get("http://localhost:3000/users/" + id).then(response => {
        if (response.status === 200) {
          this.customer = response.data;
        }
      });
    },
    updataCustomer() {
      if (!this.customer.name || !this.customer.phone || !this.customer.emali) {
        this.alert = "请添加对应信息";
        return;
      } else {
        let updataCustomer = {
          name: this.customer.name,
          phone: this.customer.phone,
          emali: this.customer.emali,
          education: this.customer.education,
          graduationschool: this.customer.graduationschool,
          profession: this.customer.profession,
          profile: this.customer.profile
        };
        this.axios
          .put(
            "http://localhost:3000/users/" + this.$route.params.id,
            updataCustomer
          )
          .then(response => {
            // console.log(response);
            this.$router.push({
              path: "/",
              query: { alert: "用户信息更新成功！" }
            });
          })
          .catch(function(err) {
            console.log(err);
          });
      }
    }
  },
  components: {
    Alert
  },
  created() {
    this.fetchCustomer(this.$route.params.id);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
