<template>
  <div class="home">
    <Todolist />
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import Todolist from "@/components/Todolist.vue";

export default {
  name: "Home",
  components: {
    Todolist,
  },
};
</script>
