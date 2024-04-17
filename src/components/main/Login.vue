<script setup>
</script>

<script>
export default {
  props: [],
  data() {
    return {
    };
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    }, 
    login() {
      // TODO 로그인

      // 후처리
      alert("Log in success");
      this.$emit("doCtrlLogin");
      this.move("Welcome");
    }
  },
  mounted() {
    
  }
};
</script>

<template>
  <table>
    <tr>
      <label>
        <th>ID : </th>
        <td><input type="text"/></td>
      </label>
    </tr>
    <tr>
      <label>
        <th>PW : </th>
        <td><input type="password"/></td>
      </label>
    </tr>
    <tr class="btnRow">
      <td colspan="2"><button v-on:click="login">로그인</button></td>
    </tr>
    <tr class="btnRow">
      <td colspan="2"><button v-on:click="move('Signup')">회원가입</button></td>
    </tr>
  </table>
</template>

<style>
th {
  width: 100px;
  text-align: right;
}
.btnRow {
  text-align: center;
}
button {
  width: 150px;
  cursor: pointer;
}
</style>
