<script>
export default {
  props: ["axios", "retrieveParam"],
  data() {
    return {
      bookList: [],
      searchParam: {
        pageNo: 1,
        value: '',
        pageCnt: 1
      }, 
      searchValue: '',
    };
  },
  methods: {
    writeBook() {
      this.$emit("moveBoardComp", "Write");
    },
    retrieveBookList() {
      this.searchParam.pageNo = this.searchParam.pageNo < 1 ? 1 : this.searchParam.pageNo;
      this.searchParam.pageNo = this.searchParam.pageNo > this.searchParam.pageCnt ? this.searchParam.pageCnt : this.searchParam.pageNo;
      this.axios({
        method: 'post', 
        url: "/board/retrieveBookList", 
        data: {
          searchParam: this.searchParam
        }
      })
      .then((response) => {
        let data = response.data;
        this.bookList = data.bookList;
        this.searchParam.pageCnt = data.pageCnt;
      })
      .catch((error) => {
        console.error(error);
      })
      .finally(() => {
      });
    }, 
    searchBookList() {
      this.searchParam.value = this.searchValue;
      this.searchParam.pageNo = 1;
      this.retrieveBookList();
    }, 
    onBtnPnoClick(pageNo) {
      this.searchParam.pageNo = pageNo;
      this.retrieveBookList();
    }, 
    doBookTitleClick(bookNo) {
      this.$emit("doOpenBook", bookNo, this.searchParam);
    }
  }, 
  mounted() {
    this.searchParam = this.retrieveParam;
    this.retrieveBookList();
  }
};
</script>

<template>
  <div class="bookList">
    <div class="toolRow">
      <div class="leftTool">
        <input type="text" v-model="searchValue" />
        <button v-on:click="searchBookList">검색</button>
      </div>
      <div class="rightTool">
        <button v-on:click="writeBook">글쓰기</button>
      </div>
    </div>
    <template v-if="bookList.length > 0">
      <table>
        <tr>
          <th>번호</th>
          <th>제목</th>
          <th>작성자</th>
          <th>작성일</th>
          <th>조회수</th>
        </tr>
        <tr v-for="book in bookList">
          <td>{{ book.idx }}</td>
          <td v-on:click="doBookTitleClick(book.idx)" class="bookTitle">{{ book.title }}</td>
          <td>{{ book.creaId }}</td>
          <td>{{ book.creaDtm }}</td>
          <td>{{ book.hitCnt }}</td>
        </tr>
      </table>
      <div class="pagination">
        <button v-on:click="onBtnPnoClick(1)"><<</button>
        <button v-on:click="onBtnPnoClick(searchParam.pageNo % 10 === 0 ? searchParam.pageNo - 10 : searchParam.pageNo-(searchParam.pageNo%10))"><</button>
        <template v-for="n in searchParam.pageCnt">
          <template v-if="(searchParam.pageNo % 10 === 0 && n > searchParam.pageNo - 10 && n <= searchParam.pageNo) || (searchParam.pageNo % 10 !== 0 && n > searchParam.pageNo - (searchParam.pageNo%10) && n <= searchParam.pageNo - (searchParam.pageNo%10) + 10)">
            <span v-if="n === searchParam.pageNo">{{ n }}</span>
            <button v-else v-on:click="onBtnPnoClick(n)">{{ n }}</button>
          </template>
        </template>
        <button v-on:click="onBtnPnoClick(searchParam.pageNo % 10 === 0 ? searchParam.pageNo + 1 : searchParam.pageNo-(searchParam.pageNo%10)+11)">></button>
        <button v-on:click="onBtnPnoClick(searchParam.pageCnt)">>></button>
      </div>
    </template>
    <div v-else>게시글이 없습니다.</div>
  </div>
</template>

<style>
.bookList{
  flex: 1 0 600px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.bookList table {
  min-width: 100%;
}
.bookList th {
  text-align: center;
}
.bookList .toolRow {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 10px;
}
.bookList .leftTool {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  gap: 10px;
}

.bookList .pagination {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 10px;

}

.bookList .bookTitle {
  cursor: pointer;
}
</style>
