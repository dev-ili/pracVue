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
    signup() {
      // TODO 회원가입

      // 성공시 후처리
      alert("Sign up success");
      this.move('Login');
    }
  },
  mounted() {
    
  }
};
</script>

<template>
  <table class="signup">
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
    <tr>
      <label>
        <th>PW 확인: </th>
        <td><input type="password"/></td>
      </label>
    </tr>
    <tr>
      <label>
        <th>e-mail: </th>
        <td><input type="email"></td>
      </label>
    </tr>
    <tr class="btnRow">
      <td colspan="2" v-on:click="signup"><button>회원가입</button></td>
    </tr>
    <tr class="btnRow">
      <td colspan="2"><button v-on:click="move('Login')">취소</button></td>
    </tr>
  </table>
</template>

<style>
.signup th {
  width: 100px;
  text-align: right;
}
.signup .btnRow {
  text-align: center;
}
.signup button {
  width: 150px;
}
</style>
