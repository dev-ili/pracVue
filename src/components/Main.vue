<script setup>
import Welcome from "./main/Welcome.vue";
import Board from "./main/Board.vue";
import Login from "./main/Login.vue";
import Signup from "./main/Signup.vue";
</script>

<script>
export default {
  props: ["currComp", "isLogin"],
  components: {
    Welcome,
    Board,
    Login,
    Signup,
  },
  data() {
    return {};
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    }, 
    doCtrlLogin() {
      this.$emit("doCtrlLogin");
    }
  },
  mounted() {
  }
};
</script>

<template>
  <main>
    <component class="main" :is="currComp" v-on:move="move" v-on:doCtrlLogin="doCtrlLogin"></component>
  </main>
</template>

<scrip>
</scrip>

<style>
main {
  min-height: 600px;
}
</style>
