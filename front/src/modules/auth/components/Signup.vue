<template>
  <div class="auth">
    <form v-on:submit.prevent>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <h1 class="heading-primary">{{ title }}</h1>
          <hr>
          <div class="form-group">
            <label for="username">Username <span>*</span> </label>
            <input v-model="user.username" id="username" class="form-control" name="username" type="email" placeholder="email@example.com" required>
            <!-- <input v-model="user.password" id="password" name="password" type="password" placeholder="password" pattern=".{5,10}" title="5 to 10 characters" required> -->
          </div>
          <div class="form-group" >
            <label for="password">Password <span>*</span> </label>
            <input v-model="user.password" id="password" class="form-control" name="password" type="password" placeholder="Enter a valid password" required>
          </div>
          <div class="form-group">
            <label for="firstName">FirstName   </label>
            <input v-model="user.firstName" id="firstName" class="form-control" name="firstName" type="text" placeholder="...">
          </div>
          <div class="form-group">
            <label for="lastName">LastName   </label>
            <input v-model="user.lastName" id="lastName" class="form-control" name="lastName" type="text" placeholder="...">
          </div>
          <router-link tag="button" class="btn btn-lg btn--white":to="{name:'login'}">Go to Login</router-link>
          <button class="btn btn-lg btn--white" @click="signIn">Sign In</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import swal from "sweetalert2";

export default {
  name: "signup",
  data() {
    return {
      title: "Signup to OurAwesomeApp",
      user: {
        username: "",
        email: "",
        password: "",
        message: ""
      }
    };
  },
  methods: {
    signIn() {
      this.$http
      .post("/auth/signup", this.user)
      .then(res => {
        if (res) {
          swal({
            type: "success",
            title: "Congrat !",
            text: res.data.message
          });
          this.$router.push("/login");
        } else {
          swal({
            type: "error",
            text: "Server Error"
          });
        }
      })
      .catch(error => {
        if (error) {
          swal({
            type: "error",
            title: "Oh no ...",
            text: error.response.data.message
          });
        } else {
        }
      });
    }
  }
};
</script>

<style scoped>
</style>
