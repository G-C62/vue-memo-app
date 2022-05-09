<template>
  <div class="memo-app">
    <memo-form @addMemo="addMemo" />
    <ul class="memo-list">
      <memo
        v-for="memo in memos"
        :key="memo.id"
        :memo="memo"
        @deleteMemo="deleteMemo"
        @updateMemo="updateMemo"
        :editingId="editingId"
        @setEditingId="SET_EDITING_ID"
        @resetEditingId="RESET_EDITING_ID"
      />
    </ul>
  </div>
</template>
<script>
import axios from "axios";
import MemoForm from "./MemoForm.vue";
import Memo from "./Memo.vue";
import { mapActions, mapState, mapMutations } from "vuex";
import { RESET_EDITING_ID, SET_EDITING_ID } from "../store/mutations-types";

const memoAPICore = axios.create({
  baseURL: "http://localhost:8000/api/memos",
});

export default {
  name: "MemoApp",
  methods: {
    updateMemo(payload) {
      const { id, content } = payload;
      const targetIndex = this.memos.findIndex((v) => v.id === id);
      const targetMemo = this.memos[targetIndex];
      memoAPICore.put(`/${id}`, { content }).then(() => {
        this.memos.splice(targetIndex, 1, { ...targetMemo, content });
      });
    },
    ...mapActions(["fetchMemos", "addMemo", "deleteMemo", "updateMemo"]),
    ...mapMutations([SET_EDITING_ID, RESET_EDITING_ID]),
  },
  computed: {
    ...mapState(["memos", "editingId"]),
  },
  components: {
    MemoForm,
    Memo,
  },
  created() {
    this.fetchMemos();
  },
};
</script>
<style scoped>
.memo-list {
  padding: 20px 0;
  margin: 0;
}
</style>
