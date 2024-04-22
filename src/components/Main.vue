<script setup>
import Welcome from "./main/Welcome.vue";
import Board from "./main/Board.vue";
import Login from "./main/Login.vue";
import Signup from "./main/Signup.vue";
</script>

<script>
export default {
  props: ["mainComp", "isLogin", "axios"],
  components: {
    Welcome,
    Board,
    Login,
    Signup
  },
  data() {
    return {};
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    },
    doCtrlLogin(dto) {
      this.$emit("doCtrlLogin", dto);
    },
  },
  mounted() {},
};
</script>

<template>
  <main>
    <component
      :is="mainComp"
      v-on:move="move"
      v-on:doCtrlLogin="doCtrlLogin"
      v-bind:axios="axios">
    </component>
  </main>
</template>

<scrip>
</scrip>

<style>
main {
  min-height: 600px;
}
</style>
