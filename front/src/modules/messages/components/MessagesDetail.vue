<template>
  <div class="col-xs-12">
    <div class="messagesdetails">
      <h2 class="heading-secondary">{{ $route.params.message.title }}</h2>
      <p>From: {{ $route.params.message.senderId }}</p>
      <div class="content">{{ $route.params.message.content }}</div>
    </div>
  </div>
</template>

<script>
import swal from "sweetalert2";

export default {
  name: "messagesDetail",
  data() {
    return {
      messages: []
    };
  },
  methods: {
    update(id) {
      let _readDate = Date.now();
      if (this.$route.params.message.read === false) {
        this.$http
          .put("/messages/" + id, { readDate: _readDate })
          .then(res => {})
          .catch(error => {
            if (error)
              swal({
                type: "error",
                title: "Oh no ...",
                text: error.response.data.message
              });
          });
      }
    }
  },
  beforeMount() {
    let id = this.$route.params.ID;
    this.update(id);
  }
};
</script>

<style scoped>
.content {
  white-space: normal;
}
</style>
