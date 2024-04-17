<script setup>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";
</script>

<script>
export default {
  components: { Header, Main, Footer },
  data() {
    return {
      mainComp: "Welcome",
      isLogin: false,
    };
  },
  methods: {
    move(page) {
      if(this.isLogin && (page == "Login" || page == "Signup")) {
        page = "Welcome";
      } else if(!this.isLogin && !(page == "Login" || page == "Signup")){
        page = "Login";
      }
      this.mainComp = page;
      console.log(this.mainComp);
    },
    doCtrlLogin() {
      this.isLogin = !this.isLogin;
    }
  },
  mounted() {
    if(!this.isLogin) {
      this.mainComp = "Login";
    }
  }
};
</script>

<template>
  <Header v-if="isLogin" v-on:move="move" v-on:doCtrlLogin="doCtrlLogin"></Header>
  <Main v-bind:isLogin="isLogin" v-bind:currComp="mainComp" v-on:move="move" v-on:doCtrlLogin="doCtrlLogin"></Main>
  <Footer></Footer>
</template>

<style>
* {
  border: 1px solid #f00;
}
</style>
