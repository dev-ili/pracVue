<script setup></script>

<script>
export default {
  props: ["axios"],
  data() {
    return {
      id: "",
      pw: "",
      pw2: "",
      name: "",
      nickNm: "",
      tel: "",
      eMail: "",
    };
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    },
    signup() {
      if (this.id == null || this.id.length === 0
      || this.pw == null || this.pw.length === 0
      || this.name == null || this.name.length === 0
      || this.tel == null || this.tel.length === 0
      || this.eMail == null || this.eMail.length === 0) {
        alert("필수값을 입력하세요.");
      } else if(this.pw !== this.pw2) {
        alert("비밀번호를 확인하세요.");
      } else {
        // TODO 회원가입
        this.axios({
          method: "post",
          url: "/member/signup",
          data: {
            id: this.id,
            passWd: this.pw,
            name: this.name,
            nickNm: this.nickNm,
            tel: this.tel,
            eMail: this.eMail,
          },
        })
        .then((response) => {
          let data = response.data;
          if(data.res === "succ") {
            alert("Sign up success");
            this.move('Login');
          } else if(data.res === "fail") {
            alert("이미 존재하는 ID");
          }
        })
        .catch((error) => {})
        .finally(() => {});
  
      }
    },
  },
  mounted() {},
};
</script>

<template>
  <div class="signup">
    <table>
      <tr>
        <label>
          <th>*ID :</th>
          <td><input type="text" v-model="id" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>*PW :</th>
          <td><input type="password" v-model="pw" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>*PW 확인 :</th>
          <td><input type="password" v-model="pw2" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>*이름 :</th>
          <td><input type="text" v-model="name" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>닉네임 :</th>
          <td><input type="text" v-model="nickNm" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>*전화번호 :</th>
          <td><input type="tel" v-model="tel" /></td>
        </label>
      </tr>
      <tr>
        <label>
          <th>*e-mail :</th>
          <td><input type="email" v-model="eMail" /></td>
        </label>
      </tr>
      <tr class="btnRow">
        <td colspan="2" v-on:click="signup"><button>회원가입</button></td>
      </tr>
      <tr class="btnRow">
        <td colspan="2"><button v-on:click="move('Login')">취소</button></td>
      </tr>
    </table>
  </div>
</template>

<style>
.signup table {
  margin: auto;
}
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
