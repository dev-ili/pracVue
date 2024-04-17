<script>
export default {
  props: [
  ],
  data() {
    return {
      books: [],
      randNo: Math.round(Math.random()*1000000),
    };
  },
  methods: {
    addBook() {
      this.randNo++;
      let book = {
        bno: this.randNo,
        title: "test" + this.randNo,
        author: "tester",
        creaDtm: new Date(),
        cnt: Math.round(Math.random()*100)
      };
      this.books.push(book);
      this.book
    },
    delBooks() {
      this.books = [];
    },
  }, 
  mounted() {
  }
};
</script>

<template>
  <div class="board">
    <div>
      <button v-on:click="addBook">글쓰기</button>
      <button v-on:click="delBooks">글목록전체제거</button>
    </div>
    <table v-if="books.length > 0">
      <tr>
        <th>번호</th>
        <th>제목</th>
        <th>작성자</th>
        <th>작성일</th>
        <th>조회수</th>
      </tr>
      <tr v-for="book in books">
        <td>{{ book.bno }}</td>
        <td>{{ book.title }}</td>
        <td>{{ book.author }}</td>
        <td>{{ book.creaDtm }}</td>
        <td>{{ book.cnt }}</td>
      </tr>
    </table>
    <div v-else>게시글이 없습니다.</div>
  </div>
</template>

<style>
.board {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.board th {
  text-align: center;
}
</style>
