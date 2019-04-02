<template>
  <Main />
</template>

<script lang="ts">
import Vue from "vue";
import Main from "@/components/Main.vue"; // @ is an alias to /src

export default Vue.extend({
  name: "home",
  components: {
    Main
  }
});
</script>
