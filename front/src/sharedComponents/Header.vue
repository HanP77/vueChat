<template>
  <nav class="navbar navbar-default ournav" id="background">
    <div class="container">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <div>
          <ul class="nav navbar-nav">
            <li><a href="#" class="navbar-brand" id="vueChat" v-on:click="routerVueChat">vueChat</a></li>
          </ul>
        </div>
      </div>
      <div id="navbar" class="collapse navbar-collapse">
        <ul class="nav navbar-nav">
          <router-link tag="li" :to="{name: 'welcome'}"><a>Home</a></router-link>
          <router-link tag="li" :to="{name: 'userList'}"><a>Users</a></router-link>
          <router-link tag="li" :to="{name: 'messagesList'}"><a>Your Inbox</a></router-link>
          <router-link tag="li" :to="{name: 'sendMessages'}"><a>Send a message</a></router-link>
        </ul>
        <ul class="nav navbar-nav navbar-right">
          <router-link tag="li" :to="{name: 'profileEdit'}"><a>{{ User }}</a></router-link>
          <li><a href="#" v-on:click="routerLogout">Logout</a></li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import swal from "sweetalert2";

export default {
  name: "Header",
  data() {
    return {
      User: localStorage.getItem("User")
    };
  },
  methods: {
    routerVueChat() {
      swal({
        title: "Get out (╯°□°）╯︵ ┻━┻",
        width: 345,
        background:
        '#fff url("https://media.giphy.com/media/RrVzUOXldFe8M/giphy.gif")',
        padding: 65,
        backdrop: `rgba(0,0,123,0.4) url("") center right no-repeat`
      });
      this.$router.push("/home");
    },
    routerLogout() {
      localStorage.removeItem("Clef");
      localStorage.removeItem("User");
      this.$router.push("/login");
    },
    Token() {
      let getToken = localStorage.getItem("Clef");
      if (getToken === null) {
        this.$router.push("/login");
      }
    }
  },
  created() {
    this.Token();
  }
};
</script>

<style scoped>

</style>