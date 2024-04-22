<script>
export default {
  props: ["axios"],
  data() {
    return {
      book: {
        title: "",
        contents: "",
      },
    };
  },
  methods: {
    onBtnSaveClick() {
      console.log(this.book);
      this.axios({
        method: "post",
        url: "/board/saveBook", 
        data: {
          book: this.book
        }
      })
        .then((response) => {})
        .catch((err) => {
          console.error(err);
        })
        .finally(() => {});
    },
    moveBoardComp(boardComp) {
      this.$emit("moveBoardComp", boardComp);
    },
  },
  mounted() {},
};
</script>

<template>
  <div class="write">
    <div class="writeHeader">
      <input type="text" placeholder="제목" v-model="book.title" class="writeTitle" />
    </div>
    <div class="writeContents">
      <div>
        <textarea placeholder="내용" v-model="book.contents" class="writeContents"></textarea>
      </div>
    </div>
    <div class="btnRow">
      <button v-on:click="onBtnSaveClick">저장</button>
      <button v-on:click="moveBoardComp('BookList')">목록</button>
    </div>
  </div>
</template>

<style>
.write {
  width: 100%;
}
.write .writeHeader {
  display: flex;
  justify-content: row;
}
.write .writeHeader .writeTitle {
  flex: 1 0 300px;
  width: 100%;
}
.write .writeContents {
  min-height: 400px;
  margin: 10px 0;
  width: 100%;
  resize: none;
}
.write .btnRow {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin: 10px 0;
}
.write .btnRow button {
  display: inline-block;
  width: 80px;
  height: 30px;
}
</style>
