<script>
export default {
  data() {
    return {
      msg: "Here is Welcome Page",
    };
  },
  mounted() {
    console.log(this.msg);
  },
};
</script>

<template>
  <h1>hello!! {{ msg }}</h1>
</template>
