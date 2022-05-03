<template>
  <div class="memo-app">
    <memo-form />
    <memo />
  </div>
</template>
<script>
import MemoForm from './MemoForm.vue';
import Memo from './Memo.vue';

export default {
  name: 'MemoApp',
  data () {
    return {
      memos: [],
    };
  },
  created () {
    this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
  }
}
</script>