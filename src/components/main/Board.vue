<script setup>
import BookList from "./board/BookList.vue";
import Book from "./board/Book.vue";
import Write from "./board/Write.vue";
</script>

<script>
export default {
  props: ["axios"],
  components: {
    BookList,
    Book,
    Write
  },
  data() {
    return {
      boardComp: "BookList",
      bookNo: 0,
      retrieveParam: {
        pageNo: 1,
        value: '',
        pageCnt: 1
      }
    };
  },
  methods: {
    moveBoardComp(comp) {
      this.boardComp = comp;
    },
    doOpenBook(bookNo, retrieveParam) {
      this.bookNo = bookNo;
      this.retrieveParam = retrieveParam;
      this.moveBoardComp("Book");
    },
  },
  mounted() {},
};
</script>

<template>
  <div class="board">
    <aside class="boardList">
      <div>게시판 목록</div>
    </aside>
    <component
      :is="boardComp"
      v-bind:axios="axios"
      v-bind:retrieveParam="retrieveParam"
      v-on:doOpenBook="doOpenBook"
      v-bind:bookNo="bookNo"
      v-on:moveBoardComp="moveBoardComp">
    </component>
  </div>
</template>

<style>
.board {
  display: flex;
}
.board .boardList {
  flex: 0 0 200px;
}
</style>
