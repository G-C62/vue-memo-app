<template>
  <div class="post-list-page">
    <h1>포스트 게시글</h1>
    <post-list :posts="posts" />
  </div>
</template>
<script>
import PostList from "../components/PostList.vue";
import { mapActions, mapState } from "vuex";

export default {
  components: { PostList },
  name: "PostListPage",
  created() {
    this.fetchPostList();
  },
  methods: {
    ...mapActions(["fetchPostList"])
  },
  computed: {
    ...mapState(["posts"])
  }
};
</script>
<style lang=""></style>
