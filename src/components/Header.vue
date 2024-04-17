<script>
export default {
  props: [],
  data() {
    return {};
  },
  methods: {
    move(page) {
      this.$emit("move", page);
    },
    doCtrlLogin() {
      alert("Log out Success");
      this.$emit("doCtrlLogin");
      this.move("Login");
    }
  },
  mounted() {},
};
</script>

<template>
  <header>
    <div class="nav">
      <span class="button" v-on:click="move('Welcome')">로고</span>
      <span class="button" v-on:click="move('Board')">게시판</span>
    </div>
    <div class="userSlot">
      <span class="button userSlot" v-on:click="doCtrlLogin">로그아웃</span>
    </div>
  </header>
</template>

<style>
header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
header .nav {
  display: flex;
  flex-direction: row;
  gap: 10px;
}
header .button {
  padding: 10px;
}
</style>
