<script setup>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Test1 from './components/Test1.vue'
import Test2 from './components/Test2.vue'
</script>

<script>
export default {
  components: {
    Test1,
    Test2
  }, 
  data() {
    return {
      currComp: "Test1", 
    }
  }, 
  methods: {
    doChangeComp() {
      switch(this.currComp) {
        case "Test1":
          this.currComp = "Test2";
          break;
        case "Test2":
          this.currComp = "Test1";
          break;
      }
    }
  }
}
</script>

<template>
  <Header></Header>
  <main>
    <component :is="currComp" class="main"></component>
    <button v-on:click="doChangeComp">change</button>
  </main>
  <Footer></Footer>
</template>

<style>
* {
  border: 1px solid #f00;
}
</style>