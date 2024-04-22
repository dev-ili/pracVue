<script>
export default {
  props: ["axios", "bookNo"],
  data() {
    return {
      book: {
        idx: 0,
        title: "",
        author: "",
        creaDtm: "",
        hitCnt: 0,
        contents: "",
      },
    };
  },
  methods: {
    retrieveBook() {
      this.axios({
        method: "get",
        url: "/board/retrieveBook",
        params: {
          idx: this.idx,
        },
      })
        .then((response) => {
          let data = response.data;
          if (data.errCode == 0) {
            this.book = data.book;
          } else if (data.errCode < 0) {
            alert(data.errMsg);
            this.moveBoardComp("BookList");
          }
        })
        .catch((err) => {
          console.error(err);
        })
        .finally(() => {});
    },
    moveBoardComp(boardComp) {
        this.$emit("moveBoardComp", boardComp);
    }
  },
  mounted() {
    this.idx = this.bookNo;
    this.retrieveBook();
  },
};
</script>

<template>
  <div class="book">
    <div class="bookHeader">
      <div class="bookTitle">{{ book.title }}</div>
      <div class="bookSubInfo">
        <div class="bookCreaDtm">{{ book.creaDtm }}</div>
        <div class="bookAuthor">{{ book.author }}</div>
        <div class="bookHitCnt">{{ book.hitCnt }}</div>
      </div>
    </div>
    <div class="bookContents">{{ book.contents }}</div>
    <div class="btnRow">
        <button>수정</button>
        <button>삭제</button>
        <button v-on:click="moveBoardComp('Write')">글쓰기</button>
        <button v-on:click="moveBoardComp('BookList')">목록</button>
    </div>
    <div>reply</div>
  </div>
</template>

<style>
.book {
  width: 100%;
}
.book .bookHeader {
  display: flex;
  justify-content: row;
}
.book .bookHeader .bookTitle {
  flex: 1 0 300px;
}
.book .bookHeader .bookSubInfo {
  flex: 0 0 200px;
}
.book .bookContents {
  min-height: 400px;
  margin: 10px 0;
}
.book .btnRow {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
    margin: 10px 0
}
.book .btnRow button {
    display: inline-block;
    width: 80px;
    height: 30px;
}
</style>
