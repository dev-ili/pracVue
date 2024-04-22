<script setup>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";
</script>

<script>
import axios from "axios";
export default {
  components: { Header, Main, Footer },
  data() {
    return {
      mainComp: "Welcome",
      isLogin: false,
      myAxios: axios.create({
        baseURL: "//localhost:8080",
        withCredentials: true,
        headers: {
          "Content-Type": "application/json",
        },
      }),
    };
  },
  methods: {
    move(page) {
      if (this.isLogin && (page == "Login" || page == "Signup")) {
        page = "Welcome";
      } else if (!this.isLogin && !(page == "Login" || page == "Signup")) {
        page = "Login";
      }
      this.mainComp = page;
    },
    doCtrlLogin(dto) {
      if (this.isLogin) {
        this.myAxios({
          method: "get",
          url: "/member/logout",
          data: {},
        })
          .then((response) => {
            let data = response.data;
            this.isLogin = !this.isLogin;
            this.move("Login");
          })
          .catch((error) => {
            console.error(error);
          })
          .finally(() => {});
      } else {
        this.myAxios({
          method: "post",
          url: "/member/login",
          data: {
            id: dto.id,
            passWd: dto.passWd,
          },
        })
          .then((response) => {
            let result = response.data;
            if (result.errCode === 0) {
              if (result.data.res == "fail") {
                alert("Fail");
              } else if (result.data.res == "succ") {
                this.isLogin = !this.isLogin;
                this.move("Welcome");
              }
            }
          })
          .catch((error) => {
            console.error(error);
          })
          .finally(() => {});
      }
    },
  },
  mounted() {
    if (!this.isLogin) {
      this.mainComp = "Login";
    }
  },
};
</script>

<template>
  <Header v-if="isLogin" v-on:move="move" v-on:doCtrlLogin="doCtrlLogin">
  </Header>
  <Main
    v-bind:isLogin="isLogin"
    v-bind:mainComp="mainComp"
    v-bind:axios="myAxios"
    v-on:move="move"
    v-on:doCtrlLogin="doCtrlLogin">
  </Main>
  <Footer></Footer>
</template>

<style>
* {
  border: 1px solid #f00;
}
</style>
