<template lang="">
  <div class="sign-in-page">
    <h3>로그인</h3>
    <signin-form @submit="onSubmit" />
  </div>
</template>
<script>
import SigninForm from "@/components/SigninForm";
import { mapActions } from "vuex";

export default {
  name: "Signin",
  components: {
    SigninForm
  },
  methods: {
    onSubmit(payload) {
      this.signin(payload).then(res => {
        alert("로그인이 완료되었습니다.");
        this.$router.push({ name: "PostListPage" });
      });
      // .catch(err => {
      //   alert(err.response.data.msg);
      // });
    },
    ...mapActions(["signin"])
  }
};
</script>
<style lang=""></style>
