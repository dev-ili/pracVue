<script setup>
</script>

<script>
export default {
  props: ["axios"],
  data() {
    return {
      id:'',
      passWd:''
    };
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    }, 
    login() {
      let dto = {
        id: this.id, 
        passWd: this.passWd
      }
      this.$emit("doCtrlLogin", dto);
    }
  },
  mounted() {
    
  }
};
</script>

<template>
  <div class="login">
    <table>
      <tr>
        <label>
          <th>ID : </th>
          <td><input type="text" v-model="id"/></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>PW : </th>
          <td><input type="password" v-model="passWd"/></td>
        </label>
      </tr>
      <tr class="btnRow">
        <td colspan="2"><button v-on:click="login">로그인</button></td>
      </tr>
      <tr class="btnRow">
        <td colspan="2"><button v-on:click="move('Signup')">회원가입</button></td>
      </tr>
    </table>
  </div>
</template>

<style>
.login table {
  margin: auto;
}
.login th {
  width: 100px;
  text-align: right;
}
.login .btnRow {
  text-align: center;
}
.login button {
  width: 150px;
  cursor: pointer;
}
</style>
