<template>
  <div class="post-view-page">
    <post-view v-if="post" :post="post" />
    <p v-else>게시글 불러오는 중...</p>
    <router-link :to="{ name: 'PostListPage' }">목록</router-link>
  </div>
</template>
<script>
import { mapActions, mapState } from "vuex";
import PostView from "@/components/PostView";

export default {
  name: "PostViewPage",
  components: {
    PostView
  },
  methods: {
    ...mapActions(["fetchPost"])
  },
  props: {
    postId: {
      type: String,
      required: true
    }
  },
  computed: {
    ...mapState(["post"])
  },
  created() {
    this.fetchPost(this.postId).catch(err => {
      alert(err.response.data.msg);
      this.$router.back();
    });
  }
};
</script>
<style lang=""></style>
