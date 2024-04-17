<script>
export default {
    data() {
        return {
            books: [],
        }
    }
}
</script>

<template>
  <table v-if="books.length > 0">
    <tr>
      <th>번호</th>
      <th>제목</th>
      <th>작성자</th>
      <th>작성일</th>
      <th>조회수</th>
    </tr>
    <tr v-for="book in books"></tr>
  </table>
  <div v-else>게시글이 없습니다.</div>
  
</template>
<style></style>
